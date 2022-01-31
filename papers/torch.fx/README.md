# TORCH.FX: PRACTICAL PROGRAM CAPTURE AND TRANSFORMATION FOR DEEP LEARNING IN PYTHON

Reed, James K., et al. "torch. fx: Practical Program Capture and Transformation for Deep Learning in Python." arXiv preprint arXiv:2112.08429 (2021).

## Notes

- Ways to capture program structure:
  - Tracing: Trace the execution of a model given some example inputs and record the operations that occur (**jit.trace**).
  - Symbolic Tracing: Tracing with abstract values rather than example inputs (tf.function). This approach surfaces locations where Python control flow depends on the input values, rather than collecting a trace specialized to the control decisions imparted by the example inputs.
  - Writing models directly in an embedded programming language (TorchScript).

- IR Design:
  - Many frameworks define their IR in a cross language way (Tensorflow uses protocol buffers)
  - PyTorch’s JIT uses C++ data structures for their IR with additional bindings into Python
  - Most neural networks are expressible as flat sequences of tensor operations (basic block) without control flow such as if-statements or loops. Basic block programs are often represented as a directed acyclic graph (DAG) data structure.

- Basic Block Programs:
  - MLPs
  - CNNs such as ResNet
  - Personalization/Recommender models
  - Transformer networks (barring the loop needed for sequence generation on the decoder portion)

- Non-Basic Block Programs:
  - RNNs such as LSTM and GRU because recurrent network computation is applied repeatedly across elements of a sequence with dynamic length. Can be implemented as loop with tensor computation applied in the loop body and tensor values carried across loop iterations but an entire RNN application over a sequence appears in code as a call to an RNN function or module. So we can call it Basic Block Program as well.

- torch.fx
  - Captures programs with symbolic tracing
  - Represents them using a simple 6-instruction python-based IR
  - Regenerates Python code from the IR to execute it

- Graph components:
  - **placeholder nodes** represent inputs
  - single **output node** represents the result of graph
  - **call_function** nodes have a reference directly to the Python function they would call
  - **call_method** n0des directly invoke a method on their first argument

- Uses **Proxy** data structure to record operations on values flowing through the program.
  - Proxy records attribute accesses and method calls
  - Symbol capturing is configurable via a **Tracer** class whose methods can be overridden.

- Represents programs as a DAG-based IR.
  - Nodes have string opcode describing the type of operation.
  - Nodes have an associated target for call nodes (call_module, call_function, call_method).
  - Nodes have args and kwargs which represents the arguments to the target.
  - Data dependencies between nodes are represented as references to other Nodes within args and kwargs.
  - Two opcodes for accessing state in the Module hierarchy: call_module to invoke forward method of the module and get_attr to fetch parameters of the module.