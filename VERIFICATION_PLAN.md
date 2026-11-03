# Verification and validation plan

**Draft — 2026-11-03. All tests NOT RUN.** No commands exist yet; any future commands are planned, **NOT executed**, and must be specified after implementation. [Requirements](SPEC.md), [architecture](ARCHITECTURE.md), [tasks](IMPLEMENTATION_PLAN.md), [evidence](EVIDENCE.md).

## Freeze and measurement rules

P0 exploratory conditioning and feasibility runs may change candidate models and numerical settings; label them exploratory, retain results and keep physical holdouts inaccessible. Before any scored numerical acceptance run, sign and hash the numerical `acceptance-contract` fixing cases, scales and thresholds. Before each physical assessment, separately freeze dataset versions/hashes, calibration and untouched independent holdouts, quantities, alignment, uncertainty, metrics and thresholds. The model lead proposes; an independent reviewer approves; the data steward approves access. Changes after scoring require a new contract, rationale and untouched holdout; retain prior outcomes.

**Proposed engineering defaults, not source values or physical acceptance:** start convergence experiments at relative tolerance `1e-6` with component-scaled absolute tolerances; compare to a run tightened tenfold. Propose normalized cumulative mass and energy residual limits of `1e-6`, scaled by the maximum of initial inventory magnitude, cumulative absolute boundary throughput and a declared nonzero floor. For energy, subtract the same declared reference-specific energy from `u` and `h` before forming initial inventory and throughput scales; freeze its anchor and a positive floor. Freeze scales, absolute limits, restart/output/event-time tolerances and solver norm in P0 after conditioning studies. These are not physical accuracy claims.

Report residual histories and maxima, and separate model discrepancy, instrument uncertainty and numerical error. Baseline agreement is not experiment; never validate on calibration samples. Hold out independent runs, not points from a correlated trajectory. Physical gates require measured pressure, temperature, inventory/flow and heat inputs, uncertainty and rights. Without system experiments, the assessed system claim is blocked; a verified research release may still reproduce numerical/model comparisons labeled physically unvalidated.

## Planned tests

| Test | Method and pass condition |
|---|---|
| T01 | Reject out-of-scope motion, multi-tank, filling and unsafe-use configuration; every result has required provenance and status. |
| T02 | Round-trip SI schedule; reject unordered or duplicate times, negative demand, incompatible units and non-finite inputs. |
| T03 | At approved liquid, vapor, saturation and domain-edge states, compare pinned provider with separately sourced tabulated values and thermodynamic identities; inject backend failure, unsupported phase and wrong isomer/reference. Pass frozen numerical tolerances or explicit typed failure. |
| T04 | Analytic closed and open control volumes with constant heat and known enthalpy flux: independently integrate M and U; check per-volume and system residuals and energy-reference shift invariance. |
| T05 | Initialize feasible tank and reject inconsistent or impossible states. Compare adiabatic hold, heated dormancy and extraction against analytic balance cases and an independent compatible reference with matched assumptions; converge to frozen limits. |
| T06 | Restriction and heater reduced cases: hold/zero flow, zero/positive head, known full-open pressure-flow relation and heat-to-enthalpy relation; compare independent calculations. Verify one-way closure, flashing and invalid closures. |
| T07 | Full network with smooth withdrawal: internal fluxes cancel; requested = served + unmet and actual = served + excess, including demand below, equal to and above passive flow. Verify sink accepts actual flow, inventory, energy and unsimulated remainder after termination. |
| T08 | Scheduled transitions and pressure, depletion and phase guards: before/at/after boundary, simultaneous events, zero duration and terminal stop; assert ordering, exact-once ledger and frozen event-time tolerance. |
| T09 | Force failed nonlinear solves, failed property calls and rejected steps; compare rollback with clean run. Refine step/error settings and compare state, flux integrals and event times against frozen convergence limits. |
| T10 | Resume checkpoints before, at and after an event; compare trajectory, integrals and ledger to uninterrupted run within frozen tolerances. Reject altered provider, model, schedule, reference or checkpoint version. |
| T11 | Score untouched component **and separate coupled-system** experimental holdouts against pre-frozen metrics and thresholds; report uncertainty, discrepancy, domain and all failures. Missing dataset blocks its corresponding claim. |
| T12 | Independent reviewer recreates pinned open environment and permitted examples, runs documented numerical tests and checks hashes, reports and licenses; restricted experimental data require a documented access path only for claims relying on them. |
| T13 | Exploratory P0 spike: sponsor states target flow/duration and operating ranges first; evaluate selected fluid, saturation, static head/geometry, pressure loss, tank heat, restriction and heater across candidate conditions. Demonstrate at least one positive-flow trajectory meeting those targets with liquid throughout, and boundary failures; quantify hydrostatic/energy approximation. If none exists or properties cannot resolve it, STOP and request re-scope. This is feasibility, not validation. |
| T14 | Minimal integrator: analytic smooth ODE/DAE cases test consistent initial state, accepted-step quadrature, error control/refinement and rejection without committing trial state. Full cache/event rollback is T09. |

## Traceability

| Requirement | Task(s) | Test(s) |
|---|---|---|
| CRYO-R01 | K00, K10, K60 | T01, T12 |
| CRYO-R02 | K10 | T02 |
| CRYO-R03 | K01, K11 | T03 |
| CRYO-R04 | K20 | T05 |
| CRYO-R05 | K11, K20, K30 | T04, T05, T07 |
| CRYO-R06 | K01, K20, K30, K40 | T03, T06, T08, T13 |
| CRYO-R07 | K30 | T06, T07 |
| CRYO-R08 | K30, K40 | T07, T08 |
| CRYO-R09 | K12, K40 | T14, T09 |
| CRYO-R10 | K41 | T10 |
| CRYO-R11 | K01, K50 | T11 |
| CRYO-R12 | K00, K01, K60 | T12 |
