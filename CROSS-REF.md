# CROSS-REF — mycelium-bench

Mycelium-internal dependencies only (steer handoff §6.1; external crates stay in Cargo
metadata). Pinned revs are the fixed (buildable) tips recorded by the Phase-B wave;
content hash = git tree hash of the pinned rev.

| Interface consumed | Repo | Pinned rev | Content hash | Notes |
|---|---|---|---|---|
| mycelium-cert | https://github.com/tzervas/mycelium-runtime | `ab9cee665b620ed80ab74ea61ea639817dc49077` | tree `(tree hash: fetch dep rev locally to resolve)` | Rust API of `mycelium-cert` (see monorepo `docs/api-index/INDEX.md#mycelium-cert`) |
| mycelium-core | https://github.com/tzervas/mycelium-core | `781d3fcceba82acfe6b0eb46650513bd78a2416b` | tree `(tree hash: fetch dep rev locally to resolve)` | Rust API of `mycelium-core` (see monorepo `docs/api-index/INDEX.md#mycelium-core`) |
| mycelium-interp | https://github.com/tzervas/mycelium-runtime | `ab9cee665b620ed80ab74ea61ea639817dc49077` | tree `(tree hash: fetch dep rev locally to resolve)` | Rust API of `mycelium-interp` (see monorepo `docs/api-index/INDEX.md#mycelium-interp`) |
| mycelium-l1 | https://github.com/tzervas/mycelium-l1 | `cd32a1ed7ab7d2be38c9c3047da7318d182b7a1c` | tree `(tree hash: fetch dep rev locally to resolve)` | Rust API of `mycelium-l1` (see monorepo `docs/api-index/INDEX.md#mycelium-l1`) |
| mycelium-mlir | https://github.com/tzervas/mycelium-codegen | `f144d635e970257aee5b618f8cdfaa736e2c391d` | tree `(tree hash: fetch dep rev locally to resolve)` | Rust API of `mycelium-mlir` (see monorepo `docs/api-index/INDEX.md#mycelium-mlir`) |
| mycelium-std-runtime | https://github.com/tzervas/mycelium-std-runtime | `b1770c4f8f8e00d948eb33b35b714378a13a7148` | tree `(tree hash: fetch dep rev locally to resolve)` | Rust API of `mycelium-std-runtime` (see monorepo `docs/api-index/INDEX.md#mycelium-std-runtime`) |

**Owning docs:** E-BENCH (backend differential bench harness).
**Source provenance:** extracted from `tzervas/mycelium` archive `aad96b7a…`; fixed by
the course-correction Phase B (workspace root, git pins, toolchain + supply-chain
replicas, CI v2). Full program record: monorepo
`docs/planning/course-correction-2026-07-18/PROGRAM.md`.
