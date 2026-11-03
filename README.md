# Cryogenic Systems

Design specifications for an open-runtime, mission-coupled cryogenic fuel-system modeling library.

**Status: reviewed design draft.** This repository contains specifications and implementation plans, not implemented or experimentally validated cryogenic software.

## Vision

Connect cryogenic storage, feed and thermal behavior across operational schedules while making mass/energy balances, phase limits, events and uncertainty explicit.

The proposed first version models a stationary liquid-hydrogen tank, passive restriction, optional prescribed heater and sink. Actual flow follows the physical closure; requested demand is a diagnostic with served, unmet and excess accounting. Mission integration, multiple tanks and wider thermal networks remain future phases.

## Documentation

| Document | Contents |
| --- | --- |
| [Specification](SPEC.md) | Scope, physical limits, requirements and unresolved decisions |
| [Architecture](ARCHITECTURE.md) | Property interfaces, conservative balances, flow closure and events |
| [Implementation plan](IMPLEMENTATION_PLAN.md) | Ordered tasks, dependencies and definitions of done |
| [Verification plan](VERIFICATION_PLAN.md) | Property checks, analytic cases, rollback, restart and experimental gates |
| [Evidence](EVIDENCE.md) | Existing models, primary sources, licensing and validation blockers |

## Starting point

Begin with phase P0: evaluate model reuse, property-provider suitability and a useful liquid-feed envelope. Saturated-liquid withdrawal may flash during pressure reduction; the proposed liquid-only scope must be shown feasible or revised. Component-level evidence does not establish whole-system validation.

## Contributing

Proposals concerning thermophysical models, experimental references, conservation tests and reproducible scenarios are welcome. Link contributions to requirement/task IDs. Include fluid/isomer, units, energy-reference conventions and data rights with reference cases.

This proposal excludes physical equipment control, relief-device sizing and operational clearance.

## Licensing

An open-source release is intended; a license has not yet been selected. Public visibility alone does not grant an open-source license. Property libraries, model implementations and experimental datasets retain separate terms requiring review.
