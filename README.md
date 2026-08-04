# mycelium-bench

<!-- FLEET-BADGES:BEGIN -->
[![CI](https://github.com/tzervas/mycelium-bench/actions/workflows/fleet-ci.yml/badge.svg?branch=main)](https://github.com/tzervas/mycelium-bench/actions/workflows/fleet-ci.yml?query=branch%3Amain)
[![Security](https://github.com/tzervas/mycelium-bench/actions/workflows/fleet-security.yml/badge.svg?branch=main)](https://github.com/tzervas/mycelium-bench/actions/workflows/fleet-security.yml?query=branch%3Amain)
[![Runner](https://img.shields.io/badge/runs--on-self--hosted%20podman-informational)](https://github.com/tzervas/gha-runner-ctl)
<!-- FLEET-BADGES:END -->


Component extracted from monorepo [`tzervas/mycelium`](https://github.com/tzervas/mycelium)
at archive tip `aad96b7a425710db5e91094d4fc2ca21a129e41a` (`archive/main-pre-component-transpile-2026-07-17`).

| Field | Value |
|---|---|
| **Program** | PROGRAM-SELFHOST-DECOMPOSE-2026-07-17 Phase D |
| **Source paths** | crates/mycelium-bench |
| **License** | MIT |
| **Honesty** | Extract is mechanical copy from archive; not DN-88 production-ready dogfood; guarantee tags stay Declared/Empirical until differential upgrades |

## Build

MSRV 1.96.1. All deps are git-rev pins (no monorepo path deps).

```bash
cargo test
```

## CI benchmark gate (S-BENCH-GATE)

The `bench` job in `.github/workflows/ci.yml` runs this repo's actual harness
(`cargo run --release --bin bench`) on every push/PR to `main` and asserts the resulting
`reports/latest-report.json` has `run.cases` with length > 0, uploading the report as a build
artifact. This closes a specific gap: before this job existed, no CI path invoked the harness
at all, so a green check meant nothing about benchmarking having happened — the same fail-open
shape as a `placeholder` job whose steps cannot fail. `bench` itself intentionally exits `0`
even on an empty/degenerate corpus (see `src/bin/bench.rs`); the *CI assertion*, not the
binary's own exit code, is what makes the gate meaningful — verified locally by temporarily
emptying `src/corpus.rs::corpus()`, rebuilding, and confirming the assertion (not the binary)
fails.

**What this measures:** relative wall-clock speed and cross-backend behavioural agreement of
the interpreter (trusted base), the AOT env-machine, JIT, and direct-LLVM backends over a
small (14-case) v0-calculus program corpus (`src/corpus.rs`) spanning bit/trit ops, a
certified binary<->ternary swap, flat data matches, and recursion. The `mlir-dialect` feature
stays off by default; on or off, an absent LLVM/MLIR toolchain is recorded as a graceful
`Skipped`, distinguished in the report from a hard `Error` (`src/backend.rs`).

**What this does NOT measure:** no backend here is GPU-backed today, so there is no GPU
device requirement for this harness (flagged as an open, human-owned question — see
`docs/planning/orchestration/packages/PKG-CI-TRUTH.json` in `tzervas/mycelium-lang`, risk
notes). No number produced by a single run is a performance target or a published claim
about the language (VR-5) — every timing is `Empirical` (a trial mean with its trial count),
not `Proven`/`Exact`, and is meant as a comparison point for a *later* run under the same
methodology, not a standalone result.
