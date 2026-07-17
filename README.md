# ML Platform Capabilities

Standalone capability profile repository shared by the compiler and runtime.

These profiles are declared planning inputs. They do not execute models, start runtimes, modify model weights, or report measured speedups.

## Canonicalization Status

Last verified: 2026-07-16.

Repository source/evidence HEAD before documentation refresh: `91eb3542d6c0c5a6f4f613d42f98101eb3e1f3e8`.
Canonical architecture host: `../ml-graph-compiler-runtime`.

This repository is the intended ownership home for declared capability facts, but it is not the sole source of truth today. Compiler-local target profiles currently contain richer/newer information for active Raspberry Pi CPU kernel/thread paths, AArch64 backend-codegen schedule evidence, RMSNorm exact GPU launch/candidate evidence, deployment-specific constraints, and the measured vLLM `max_num_seqs` selector input. Runtime evidence directories own measured latency, throughput, correctness, accuracy, oracle, regret, root-cause analysis, benchmark CSV/JSON/Markdown artifacts, and telemetry.

## Owns

- Declared hardware identity.
- Static hardware capabilities.
- Backend capability declarations.
- Software, driver, and Runtime capability declarations.
- Kernel/provider capability declarations.
- Platform and deployment capability declarations.
- Model/workload metadata.

## Does Not Own

- Benchmark results.
- Calibration raw samples.
- Correctness/accuracy results.
- Runtime traces.
- Oracle/regret analysis.
- Policy artifacts unless explicitly migrated and versioned.

## Current Gaps

- Raspberry Pi profile details are not fully canonicalized here.
- Runtime executable capability and deployment capability are incomplete.
- Compiler-local target profiles are richer than this repository for several P1/E3 paths.
- AArch64 schedule/codegen, RMSNorm exact GPU launch/candidate facts, runtime RMSNorm exact-dispatch benchmark facts, and vLLM `max_num_seqs` measured-policy facts have not been normalized into reusable capability-profile schemas.
- XNNPACK software/artifact requirements are documented in compiler/runtime evidence, not yet fully normalized here.
- Synchronization between compiler-local profiles and this repository is manual.

## Migration Path

Move declared facts here only when the consuming compiler/runtime code can validate the profile reference and retain evidence/provenance links externally. Do not move measured evidence into capability profiles.

## Profile Types

- Model: model identity and high-level family metadata.
- Hardware: physical device facts.
- Platform: software/hardware APIs such as CUDA or Metal.
- Backend: inference runtimes such as vLLM, TensorRT-LLM, CoreML, ONNX Runtime, and SGLang.
- Kernel: provider/library capabilities such as FlashAttention2, CUTLASS, cuBLAS, Triton, and xFormers.
- Workload: declared workload-shape inputs used by planners.
