# Implementation plan

**Draft — 2026-11-03. Nothing executed.** Requirements are in [SPEC.md](SPEC.md); proposed tests and traceability are in [VERIFICATION_PLAN.md](VERIFICATION_PLAN.md). Every task below lists dependencies, inputs, outputs, verification and definition of done (DoD). All phase gates require recorded owner sign-off and no concealed failed test.

## P0 — Feasibility and contract

**Entry:** sponsor approves scope. **Exit:** feasible liquid-feed envelope and numerical acceptance contract signed; physical-data access and contracts tracked separately, blocking only their assessment claims.

- **K00 — Baseline and rights.** Dependencies: none. Inputs: [sources](EVIDENCE.md), distribution intent and experiment owners. Outputs: adoption matrix, transitive licenses, access, rights and blockers. Verification: inspect license texts, grants, runtimes and overlap. DoD: justified open-runtime path or no build authorization. Actions: (1) compare HyTank and FullFlow reuse/build; (2) inventory licenses and access; (3) record decision and missing experimental rights.
- **K01 — Feasibility and acceptance freeze.** Dependencies: K00. Inputs: candidates, geometry, properties, references and available datasets. Outputs: feasibility report, pinned fluid/domain, numerical `acceptance-contract`, and physical assessment status. Verification: T13 exploratory phase-envelope spike; property/reference probes and independent contract review. DoD: demonstrate a useful, nonempty liquid-feed envelope or STOP for approved re-scope; numerical criteria frozen before numerical scoring. Actions: (1) sponsor states target flow/duration and ranges, then explore provider, tank, head, restriction, heat and heater feasibility; (2) condition numerical cases and freeze limits before acceptance runs; (3) identify physical datasets/rights and, when available, freeze independent holdouts, uncertainty and thresholds before physical scoring. Missing physical data blocks that claim, not the research path.

## P1 — Foundations

**Entry:** P0 signed and feasible. **Exit:** primitives and minimal stepping pass T01–T04 and T14.

- **K10 — Contracts and units.** Dependencies: K01. Inputs: frozen schema and SI rules. Outputs: configuration, schedule, outcome and typed-failure contracts. Verification: T01, T02. DoD: valid round trip and malformed input rejected with actionable diagnostics. Actions: (1) define schemas and SI conversions; (2) test valid and malformed cases.
- **K11 — Properties and balances.** Dependencies: K10. Inputs: provider feasibility, reference convention and test points. Outputs: property adapter and control-volume accounting primitives. Verification: T03, T04 including reference-shift invariance and failure injection. DoD: limits met without hidden fallback or clipping. Actions: (1) implement pinned provider contract; (2) add balance ledger; (3) check identities and injected failures.
- **K12 — Minimal integrator.** Dependencies: K11. Inputs: numerical contract and smooth analytic cases. Outputs: consistent initialization, implicit accepted-step integration, local error control, rejection of trial state, and accepted-step flux quadrature. Verification: T14. DoD: initialization, smooth convergence and rejected-state noncommit pass; event handling and full cache/ledger rollback remain K40. Actions: (1) solve consistent initial state and algebraic residuals; (2) advance and reject trial steps; (3) check refinement and quadrature.

## P2 — Isolated tank

**Entry:** P1 complete. **Exit:** initialized tank and independent reference comparisons pass T05; physical claims remain gated by the frozen data contract.

- **K20 — Tank.** Dependencies: K12. Inputs: approved equilibrium closure, domain and initial/reference cases. Outputs: rigid-tank dynamics, initialization and smooth dormancy/extraction reports. Verification: T05 against analytic balances and an independent compatible reference. DoD: cases converge and residuals pass; shared assumptions documented. Actions: (1) connect tank closure to K12; (2) run smooth hold/extraction cases; (3) compare balances and reference.

## P3 — Coupled system

**Entry:** P2 complete. **Exit:** restriction/heater/demand network passes T06 and T07 with full boundary accounting.

- **K30 — Coupling.** Dependencies: K20, K12. Inputs: component contracts and permitted ranges. Outputs: network solve, fluxes and requested/actual/served/unmet/excess reporting. Verification: T06 and T07 on smooth cases. DoD: internal fluxes cancel, sink outflow and demand reconcile, invalid states fail explicitly. Actions: (1) implement passive restriction, heater and sink closure; (2) integrate using K12; (3) compare reduced cases and shortfall/excess accounting.

## P4 — Modes and restart

**Entry:** P3 complete. **Exit:** event, boundary, rollback, convergence and restart tests T08–T10 pass.

- **K40 — Operational execution.** Dependencies: K30, K12. Inputs: schedule, guards and solver contract. Outputs: modes, event scheduler, full rollback, deterministic ledger and stop outcomes atop K12. Verification: T08, T09 including event coincidence and forced failure. DoD: no duplicated events or committed rejected-step effects; refinement thresholds pass. Actions: (1) add schedule splitting and guard roots; (2) roll back all trial side effects; (3) verify boundaries and retries.
- **K41 — Checkpoint and identity.** Dependencies: K40. Inputs: accepted state, solver and provider metadata. Outputs: versioned checkpoint and resume validation. Verification: T10 at ordinary and event boundaries, including changed-input rejection. DoD: resumed outputs match within frozen limits and mismatches fail closed. Actions: (1) serialize state, integrals and identities; (2) reject mismatches; (3) compare resumed trajectories and events.

## P5 — Independent evidence

**Entry:** P4 complete; independent held-out experimental data and signed physical acceptance contract available. **Exit:** T11 complete with independent review; failed criteria or missing access block validated claims.

- **K50 — Physical assessment.** Dependencies: K41, K01 plus assessment-specific data and contract. Inputs: frozen calibration/holdout datasets, uncertainty budgets and predictions. Outputs: separate component and end-to-end system reports, residuals, sensitivity/uncertainty and limitations. Verification: T11 against independent observations and prespecified limits. DoD: reviewer signs evidence and failures; absent system data blocks system claim. Actions: (1) acquire rights and freeze split/contract; (2) score component and separate system holdouts; (3) review uncertainty and limitations.

## P6 — Reproduction and adoption

**Entry:** P4 complete; P5 required only for the physical claims proposed. **Exit:** T12 independently reproduced and adoption authority approves the declared scope.

- **K60 — Package handoff.** Dependencies: K41, K00; K50 only for assessed claims. Inputs: source, environment lock, rights and available evidence. Outputs: open-runtime research package, permitted examples, manifest and reproduction instructions. Verification: T12 on a clean independent environment with license checks. DoD: reviewer reproduces declared outcomes and limitations; without K50 label system behavior unvalidated and make no experimental-system claim. Actions: (1) assemble pinned artifact and rights; (2) independently reproduce numerical evidence; (3) approve scope and label unsupported claims.

## Conditional future gates

Multi-tank plumbing, mission coupling, and external thermal integration are **three separate proposals**, each needing its own interface, supported regimes, risks, test/validation data, acceptance thresholds and independent approval. None follows automatically from P6.
