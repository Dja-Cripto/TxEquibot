# Roadmap

Milestones are ordered by dependency, not calendar promises.

| Milestone | Deliverable | Completion gate | Current status |
|---|---|---|---|
| 0. Proposal | Public documentation and access request | Scope, status and dependencies consistent | Documentation prepared |
| 1. Product demonstration | Three linked screens with labelled simulated data | Configure/evaluate/monitor journey understandable | Planned |
| 2. Read-only integration | Instruments, market and account views | Correct units, freshness and permissions | Planned |
| 3. Evaluation | Versioned strategy and simulated runs | Reproducible report and disclosed assumptions | Planned |
| 4. Test execution | Signed orders, reconciliation and restart recovery | Critical validation scenarios pass | Planned |
| 5. Authorized pilot | One strategy and limited instruments | Access granted, limits reviewed, records reconciled | Dependent on approval and validation |
| 6. Invited users | Small multi-user pilot | Isolation, credential protection and operational recovery verified | Planned |
| 7. Expansion | Additional strategies or cross-exchange hedging | Evidence of demand and reliable initial operation | Future |

## Decisions still open

- Initial instruments and financial limits.
- Exact entry/exit conditions and supported order types.
- Data coverage and feasible simulation fidelity.
- Hosting, maintained SDK/library choices, and credential management.
- Pilot size and request-volume estimate derived from measured usage.
- Commercial model and any user-approved Builder Code fee.

## Future cross-exchange cycles

The earlier delta-neutral concept remains documented under `integracoes/`. It includes opposite positions, independent margin monitoring, 5/12-hour configurable durations, and repeat only after both legs close. It is not implied by the single-venue MVP and will require a separate validation gate.
