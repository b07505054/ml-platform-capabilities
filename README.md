# ML Platform Capabilities

Standalone capability profile repository shared by the compiler and runtime.

These profiles are inputs to planning. They do not execute models, start runtimes,
modify model weights, or report measured speedups.

## Profile Types

- **Model**: model identity and high-level family metadata. Model weights are not stored or modified here.
- **Hardware**: physical device facts such as GPU name, VRAM, compute capability, and memory topology.
- **Platform**: software/hardware platform APIs such as CUDA or Metal. A platform is not an inference backend.
- **Backend**: inference runtimes such as vLLM, TensorRT-LLM, CoreML, ONNX Runtime, and SGLang.
- **Kernel**: provider-level kernel/library capabilities such as FlashAttention2, CUTLASS, cuBLAS, Triton, and xFormers.
- **Workload**: declared request/workload shape inputs used by planners.

## Architecture

```text
profiles/{models,hardware,platform,backend,kernels,workloads}
        |
        v
Compiler / Execution Planner
        |
        v
ExecutionPlan
        |
        v
Runtime config materializer / benchmark harness
        |
        v
Measured runtime metrics
```

The compiler consumes these profiles to produce an `ExecutionPlan` or a backend-facing exported plan such as `vllm_execution_plan.json`.
The runtime consumes the same profiles to validate and materialize runtime configuration.

Measured performance is not stored in this repository. Runtime metrics are the only measured evidence.
