# Roadmap

Milestones are ordered by dependency, not calendar promises.

| Milestone | Deliverable | Completion gate | Current status |
|---|---|---|---|
| 0. Proposal | Public documentation and access request | Scope, status and dependencies consistent | Documentation aligned 23 Oct 2026 |
| 1. Product demonstration | Interactive prototype: configure, evaluate, review, monitor, connections; simulated data; optional read-only testnet data | Configure/evaluate/monitor journey understandable; claims match status | Published 23 Oct 2026 |
| 2. Read-only integration | Instruments, funding, books and account views from TxFlow testnet, then a second venue | Correct units, freshness and permissions; public reads already shown working from a browser | Planned (testnet needs no application) |
| 3. Evaluation | Versioned strategy and reproducible runs fed by real funding and metadata | Reproducible report, disclosed assumptions, independently reconciled accounting | Simulation prototype exists; real-data feed planned |
| 4. Test execution | Signed orders on both venues' test environments, reconciliation, restart recovery, one-sided-fill recovery | Critical validation scenarios pass | Planned |
| 5. Authorized pilot | One instrument, limited size, one active cycle per user | TxFlow access granted, limits reviewed, records reconciled | Dependent on approval and validation |
| 6. Invited users | Small multi-user pilot | Isolation, credential protection and operational recovery verified | Planned |
| 7. Expansion | Additional strategies or venues, possibly a TxFlow-native hedge | Evidence of demand and reliable initial operation | Future |

## Decisions still open

- Initial instruments and financial limits (pilot caps proposed in the prototype are placeholders).
- Second venue for the hedge: Hibachi is researched; its test environment, limits and close semantics are unconfirmed. A TxFlow-native hedge (spot against perpetual) depends on a documented, stable spot API.
- Entry and exit conditions beyond the minimum-edge gate, and supported order types.
- Data coverage and feasible simulation fidelity.
- Hosting, maintained SDK/library choices, and credential management.
- Pilot size and request-volume estimate derived from measured usage.
- Commercial model: whether to charge a Builder Code fee and at what rate within TxFlow's 0.1% perpetual cap, or a software plan.

## Resolved or confirmed (23 October 2026)

- TxFlow hosts: mainnet `https://rpc.txflow.com`, testnet `https://rpc.txflow-testnet.xyz`; EIP-712 chain IDs 869 (mainnet) and 2511 (testnet); signing `apiVersion` 1; request header `x-api-version: 2026-08-16`. Mainnet writes remain subject to the limited-access phase.
- Testnet needs no application; public reads (perpMeta, activeAssetCtx, l2Book) work without credentials.
- Account setup order: deposit, approve the builder fee for the builder you trade through, approve the agent key.
- Builder Code caps and eligibility are documented (see [research](RESEARCH.md)).

## Cross-venue cycle mechanics

The hedged cycle is specified in [bot behavior](product/BOT-BEHAVIOR.md) and, in more detail, in the Portuguese notes under `integracoes/` (opposite positions, independent margin monitoring, configurable 5/12-hour durations, timer anchored on confirmed protection of both legs, repeat only after both legs close). It requires its own validation gate on every venue pair before live use.
