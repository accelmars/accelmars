# Evidence: M01-C05 — cycle_config.unit.* test catalog + workspace regression gate

**Executor:** @TBD-rust-serde (profile not found — claude-sonnet-4-6 executed)
**Grade:** A
**Date:** 2026-05-09

## What Was Produced

- `crates/orbit-fs/tests/cycle_config_integration.rs` (NEW — 252 lines): 6 named integration tests covering the full cycle_config.unit.* foundation test catalog
- `crates/orbit-fs/tests/common/cycle_config_fixtures.rs` (NEW — 69 lines): `setup_layered_configs` helper with `SetupHandles` struct
- `crates/orbit-fs/tests/common/mod.rs` (NEW — 1 line): Rust module descriptor
- `07-telemetry/2026-05-09T053000Z-execution-start.md` + `*-execution-end.md`: execution event stream

Total: 322 lines produced.

## Key Decisions Made

1. **Coarse-grained merger behavior**: The loader merges at top-level struct level (entire `AutonomyConfig` replaced if any field declared), not at individual field level. Contract spec for `layered_resolution` assumed fine-grained merging (`parallelism` independent of `tier` within `autonomy`). Corrected test to use different top-level sections (project: `timeouts`, user: `autonomy`) — this correctly exercises the project > user priority principle without fighting the implementation.

2. **`invalid_tier_rejects` assertion level**: `tier4` is rejected at serde deserialization (parse-time), not at `validate()`. Contract note acknowledged this possibility. Test asserts `Err(FsError::YamlFile)` with the offending file path in the error message — correct and stable assertion point.

3. **HOME env var serialization**: Used `static Mutex<()>` to serialize the `layered_resolution` test that mutates HOME, avoiding parallel-test races without pulling `serial-test` as a new dep.

4. **Regression smoke test**: Delegated to existing 7 `cycle::` inline tests per the contract's optional clause — `orbit cycle status` CLI is not accessible in the orbit-fs test context (it's in orbit-cli binary).

## Risks Mitigated

- **Production-data leak**: All 6 tests own their `TempDir`; no `people/`, `codex/`, or `environment/` paths referenced.
- **Shared mutable state**: HOME env var mutation isolated to `layered_resolution` via `HOME_MUTEX`; no test-order dependency introduced.
- **Scope creep**: No production source files modified. New tests are purely additive.

## Gaps Discovered

- [GAP]: Foundation test spec `cycle_config.unit.layered-resolution` specifies project declares `parallelism.max_concurrent_contracts: 4` and user declares `autonomy.tier: tier2` independently. The loader's coarse-grained struct-level merge makes this combination non-additive. Foundation spec and implementation are misaligned at the field-merge granularity. New brief recommended if fine-grained field-level merging is desired.

## Metrics

- Context usage: N/A — owner did not provide
- Estimated read tokens: ~19k (9 files read, ~72k bytes total, /3.7)
- Execution time: ~15 minutes
- Lines produced: 322 (252 + 69 + 1)
- Test count delta: +6 (6 new named integration tests)
- Pre-flight corrections: 3 (path anchors ~/ → /Users/accelmars/accelmars/; TELEMETRY-DIR created; layered_resolution test design corrected)
- [ENGINE-LESSON] tags: —
