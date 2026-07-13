# ML Platform Capabilities

Standalone capability profile repository shared by the compiler and runtime.

These profiles are inputs to planning. They do not execute models, start runtimes,
modify model weights, or report measured speedups.


## Canonicalization Status (Phase D0)

Last verified: 2026-07-13
Source host: GPU Linux `/home/allen/Desktop/Project/ml-platform-capabilities`
Verified HEAD: `84cf1d229788390f3b95254416636672fabe8d20` (`main`, origin-aligned)
Canonical architecture host: `../ml-graph-compiler-runtime`

This repository is the intended canonical source for declared capability facts, but it is not fully canonical today. Compiler-local target profiles currently contain richer and newer information for several active paths, including Raspberry Pi CPU kernel/thread descriptors and deployment-specific constraints.

Long-term ownership categories:

- declared hardware identity
- static hardware capabilities
- backend capability declarations
- software, driver, and Runtime capability declarations
- kernel/provider capability declarations
- platform and deployment capability declarations
- model/workload metadata

This repository must not become a benchmark-results database. Measured latency, throughput, correctness, accuracy, oracle, regret, telemetry, and calibration evidence belong in runtime/evaluation evidence artifacts and may be referenced by planners only with explicit truth boundaries.

Known current gaps:

- Raspberry Pi profile details are not fully canonicalized here.
- Runtime executable capability and deployment capability are incomplete.
- Compiler-local target profiles are richer than this repository for several Phase P1 paths.
- Measured evidence is intentionally absent from capability profiles.

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
