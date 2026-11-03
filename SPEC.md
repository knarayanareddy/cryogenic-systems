# Cryogenic fuel-system modeling specification

**Draft — 2026-11-03.** Future standalone research software; not implemented or validated. See [architecture](ARCHITECTURE.md), [implementation plan](IMPLEMENTATION_PLAN.md), [verification plan](VERIFICATION_PLAN.md), and [evidence](EVIDENCE.md).

## Purpose and scope

Test whether an open-runtime conservative tank-to-demand network adds operational-schedule analysis beyond existing tank and aircraft models. V1 models one stationary rigid LH2 tank, prescribed ground hold and withdrawal, passive feed restriction, optional prescribed heater and a sink. Withdrawal demand is a diagnostic, not a prescribed flow; report actual, served, unmet and excess flow. Schedules represent mission-like demand; v1 does not simulate a mission.

Exclude sloshing, acceleration, arbitrary motion, structural qualification, filling, relief-device sizing, physical control and automatic flight integration. The baseline has no vent: stop at the configured pressure limit. Multi-tank, mission and thermal integration require separate approvals. Results are research estimates, not certification or operational clearance.

## Requirements and acceptance

Each requirement is independently checked by the corresponding test in the [trace matrix](VERIFICATION_PLAN.md#traceability). Physical acceptance limits remain **unresolved**, not passed.

- **CRYO-R01 — Scope and provenance:** Reject unsupported configurations; identify assumptions, model and software versions, and intended use in every result.
- **CRYO-R02 — Units and schedules:** Accept explicit SI units and ordered, piecewise-constant ground-hold/withdrawal and heat schedules; reject negative demand, invalid time order, and inconsistent units.
- **CRYO-R03 — Properties:** A pinned, replaceable property provider shall return thermodynamically consistent state, phase, and metadata or a typed failure; define fluid isomer and reference convention.
- **CRYO-R04 — State and initialization:** Solve a consistent rigid-tank mass, energy and volume initial state; reject overdetermined or infeasible inputs, ambiguous phase, and out-of-domain states.
- **CRYO-R05 — Conservation:** Account for mass and energy at every control volume and across the system, including boundary enthalpy, heat, and work; report integrated residuals against frozen limits.
- **CRYO-R06 — Regimes:** Support the P0-approved equilibrium liquid/vapor tank envelope and liquid feed; explicitly terminate at unsupported feed phase or other excluded regimes, without clipping a state into validity.
- **CRYO-R07 — Components:** Couple tank, restriction, prescribed heater and demand using compatible port mass, pressure, enthalpy, and power; enforce component limits and expose shortfall.
- **CRYO-R08 — Events and demand:** Locate schedule changes and physical limits, log ordered transitions, and report requested, actual, served, unmet and excess mass separately; never silently supply unavailable flow.
- **CRYO-R09 — Integration:** Use error-controlled integration and consistent algebraic solves, reject and roll back failed steps, and establish convergence under refinement.
- **CRYO-R10 — Restart:** Checkpoint all state and event cursors with input/model/provider identity; reject incompatible resumes and reproduce uninterrupted trajectories to frozen tolerances.
- **CRYO-R11 — Evidence:** Separate numerical verification, model comparison, calibration and held-out component and system experiments; publish uncertainty and applicability limitations with results.
- **CRYO-R12 — Governance:** Before implementation or adoption, record license and data rights, access, independent baseline comparison, owners, frozen acceptance criteria and a release/reproduction decision; do not imply an operational clearance.

## Decisions requiring owners

P0 explores the isomer, property envelope and feed feasibility before freezing numerical acceptance; unavailable physical data block only the corresponding assessment. Before physical scoring an independent reviewer signs an assessment-specific contract and preserves untouched holdouts. P0 must demonstrate useful liquid feed or stop and seek approved re-scope. See [P0](IMPLEMENTATION_PLAN.md#p0--feasibility-and-contract) and [evidence](EVIDENCE.md).
