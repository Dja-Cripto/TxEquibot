# User experience

An interactive prototype implements the Configure, Evaluate, Review, Monitor and Connections screens with simulated evaluations and a simulated executor. It places no orders and connects no wallet. The live product screens below remain specifications until the trading integration exists.

## Design direction

A restrained financial interface with clear typography, strong spacing, readable tables and a compact set of high-priority metrics. The prototype uses a dark theme with a green accent, in the general style of the TxFlow brand, with an explicit statement that the project is independent. Color is never the only indicator of profit, risk or connection state. Desktop supports configuration; mobile supports monitoring and essential controls.

## Core screens

| Screen | Primary task | Required information |
|---|---|---|
| My bots | Understand current activity | Environment, state, open exposure on both venues, data freshness, incidents |
| Configure | Define an explicit configuration | Legs, size, hold, limits, edge gate, fees including any builder fee, assumptions |
| Evaluate | Understand a simulated result | Version, source/coverage, assumptions, costs, break-even hold, margin stress, ledger |
| Review | Authorize the intended behavior | Pre-trade checks with reasons, failure behavior, permissions, fees, stop behavior |
| Monitor | Watch and control a cycle | Both legs, net delta, margin per venue, deadline, actions with reasons, controls |
| Connections | Understand account permissions | Wallet, agent status per venue, environment, authorization and revocation steps |

## User journey

Explore a labelled prototype → configure a draft (optionally loading venue-A price, lot and funding from TxFlow's public testnet) → evaluate → inspect assumptions and the edge gate's verdict → connect/authenticate → authorize each venue's trading access → review final configuration and total fees → activate → monitor.

Connecting a wallet does not start trading. A successful login is not an agent approval. A simulation is not testnet execution, and neither is live performance.

## Essential interaction rules

- The environment label stays visible during configuration and execution, and live reads are labelled with their source and time.
- Activation requires a valid configuration, a passing review and an explicit user action. In the prototype, activation is permanently unavailable and says why.
- Missing or delayed values show as unavailable or stale, never as zero.
- A paused bot with an open position continues to display that exposure prominently.
- Amounts show currency, unit, and estimated/confirmed status. The fee a user pays on a TxFlow fill is shown as exchange fee plus builder fee, and their sum.
- When the edge gate refuses entry, the interface says so and why; refusing is a normal outcome, not an error.
- Placeholder inputs are labelled as placeholders; inputs loaded from a live read are labelled with the source.
- Changing live parameters requires a versioned update and a clear explanation of its effect on the active cycle.
- A close request remains pending until reconciled; the interface never celebrates an unconfirmed fill.
- Keyboard navigation, focus visibility, contrast and small-screen layouts are acceptance requirements.

## Prototype scope

The prototype demonstrates a configuration form with a live summary, a seeded and reproducible evaluation (net result, carry, fees, builder fee, slippage, drawdown, margin stress, hold-duration sensitivity, version save and JSON export), a pre-trade checklist, a simulated executor with distinct controls and injectable failures, and a connections screen that explains the permission model without connecting anything. It is meant to let a reviewer understand the intended product without a deposit or wallet signature.
