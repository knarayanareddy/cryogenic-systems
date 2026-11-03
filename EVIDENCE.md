# Evidence and adoption register

**Draft — 2026-11-03.** Source observations below are documentation review, not software execution, benchmark results, data access or validation. See [spec](SPEC.md), [architecture](ARCHITECTURE.md), [implementation plan](IMPLEMENTATION_PLAN.md) and [verification plan](VERIFICATION_PLAN.md).

## Primary sources reviewed

All eight exact URLs below were observed on **2026-11-03**. Recheck and pin immutable revisions before use.

1. **HyTank:** https://github.com/eytanadler/HyTank — authors describe LH2 boil-off including extraction/filling and heater operation, heat leak and tank weight; repository identifies MIT license. Direct existing baseline, not a blank space to rebuild.
2. **LLNL LH2Transfer:** https://github.com/llnl/LH2Transfer — repository describes a two-vessel lumped transfer model using MATLAB and REFPROP, and states verification is limited to typical states near/within two-phase conditions. Its NASA Open Source Agreement and dependency terms need actual review; warm-vessel cooldown is not established.
3. **DynTherM:** https://github.com/Propulsion-Power-TU-Delft/DynTherM — authors list Dymola 2022 and Modelica among prerequisites, state OpenModelica is untested, and list a hydrogen tank under development. GPL-3.0 is shown. Do not represent it as an established open-runtime tank benchmark.
4. **OpenConcept:** https://github.com/mdolab/openconcept — authors describe an OpenMDAO conceptual aircraft-design toolkit including thermal management; repository identifies MIT license. It is a possible future mission-design comparator, not proof of this network's validation.
5. **CoolProp:** https://github.com/CoolProp/CoolProp — project describes an open-source thermophysical database with multiple wrappers and identifies MIT license. Provider suitability for the selected hydrogen isomer and operating domain is not yet demonstrated.
6. **CoolProp high-level API:** https://coolprop.org/coolprop/HighLevelAPI.html — documents saturation inputs, phase ambiguity, reference states and limits on derivatives. A pinned implementation still needs feasibility and reference-consistency tests.
7. **FullFlow README:** https://github.com/saakethramoju/FullFlow — authors describe Python lumped fluid/thermal/propulsion networks, shared component states, and implicit transient dynamic/algebraic solves; it is not CFD. This is a reuse candidate, not proof of cryogenic support or validation. **License separately:** https://raw.githubusercontent.com/saakethramoju/FullFlow/HEAD/pyproject.toml declares `GPL-3.0-only`; evaluate distribution compatibility and dependencies in P0. Neither runtime nor examples were executed.

Other property packages require separate license, fluid, runtime and domain checks.

## Adoption and evidence blockers

- **Decision:** compare adapting HyTank and FullFlow against a new network and document shared algorithms or providers. Prefer reuse when fit and rights permit; independence is not assumed.
- **Data steward:** obtain tank and integrated-system experiments, uncertainty, calibration/holdout separation, access and reproduction/redistribution rights. No dataset or grant is verified here.
- **Model lead:** demonstrate a useful liquid-feed envelope including head, losses and heating, and establish isomer, references and closure validity. Runtime, `u, rho` flash and envelope are untested; stop/re-scope if infeasible.
- **Independent reviewer:** sign physical and numerical acceptance before scoring. Physical thresholds, pressure limits and experiment access remain unresolved.
- **Adoption authority:** approve license compatibility including transitive tools, then independently reproduce P6. Commercial tools may inform comparisons but cannot be required by the standalone deliverable.

## Status and self-review

All five documents are drafts; implementation, installation, publication, tests, external experiments and reproduction are **NOT RUN**. Self-review: sibling links are relative; CRYO-R01–R12 map to tasks and tests. Physical assessment needs its own signed, dataset-specific contract; missing system data blocks the assessed system claim, not a separately verified research release. No system-validation claim follows from component evidence or benchmark agreement.
