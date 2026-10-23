# TxEquibot

### Configure a trading bot. Evaluate its assumptions. Understand its execution.

TxEquibot is a proposed web application for **rule-based trading automation and transparent strategy evaluation on TxFlow**. It is being designed by an independent developer for traders who want to configure bots, review their behavior in simulation, and monitor execution through one understandable interface.

**Stage:** product specification · **Initial venue:** TxFlow · **Delivery:** web application with a persistent execution service · **Builder:** individual developer

> This repository currently contains product and engineering documentation. It does not contain a working bot, website, or live integration. Mainnet access has not been confirmed. No trading performance or existing user base is claimed.

## Start here

| Document | What it explains |
|---|---|
| [Product proposal](docs/product/PROPOSAL.md) | User problem, product value, initial scope, and why TxFlow |
| [Bot behavior](docs/product/BOT-BEHAVIOR.md) | Exactly how the first bot will enter, monitor, exit, pause, and recover |
| [User experience](docs/product/USER-EXPERIENCE.md) | Planned screens and the journey from configuration to monitoring |
| [System architecture](docs/engineering/ARCHITECTURE.md) | Execution service, integrations, persistence, and account isolation |
| [Strategy evaluation](docs/engineering/EVALUATION.md) | Simulation methodology, costs, metrics, and limitations |
| [Validation plan](docs/engineering/VALIDATION.md) | Evidence required before test and live releases |
| [Roadmap](docs/ROADMAP.md) | Milestones, deliverables, and acceptance gates |
| [Builder access request](docs/BUILDER-APPLICATION.md) | Requested capabilities, onboarding questions, and proposed pilot |
| [Research and evidence](docs/RESEARCH.md) | Official references and the distinction between facts and product hypotheses |

## The problem we want to solve

Choosing bot parameters is only the beginning. A trader also needs to understand what the bot will do, what assumptions underpin a simulated result, which costs matter, and why live execution differs from expectations.

Our product hypothesis is that a focused workflow can make these decisions easier for TxFlow users: **configure → evaluate → review → authorize → monitor**. We will validate that hypothesis with an internal pilot and a small invited group before expanding the product.

## What the first version will do

- **Configure explicit rules:** instrument, direction, entry condition, bounded position size, exit conditions, and optional repetition.
- **Evaluate before execution:** clearly labelled simulation or paper trading, with assumptions and data coverage visible.
- **Review the complete configuration:** costs, limits, permissions, and behavior during failures before activation.
- **Operate through supported APIs:** authenticated order management, streaming updates, and reconciliation of actual fills and positions.
- **Explain what happened:** order history, reason for each action, net performance, exposure, and incident status.
- **Keep controls clear:** pause new entries, stop after the current cycle, and request position closure are separate actions.

The MVP will support **one strategy family on TxFlow**, rather than promise a broad catalogue at launch. Live operation is conditional on access approval, integration validation, and explicit user activation.

## Initial strategy: bounded, rule-based position cycles

A user configures a long or short entry, a bounded size, and exit rules. A cycle can have a maximum holding duration, such as 5 or 12 hours, and optional repetition after the previous position is confirmed closed and entry checks pass again.

The timer is an execution rule, not a source of profit. A single-venue directional position is not delta neutral. Cross-exchange hedged cycles remain a **later expansion**, with separate requirements for coordinating both legs and handling incomplete hedges.

## Designed for understandable evaluation

Every evaluation will identify the strategy version, inputs, data period, costs, and execution assumptions. Historical backtesting will be offered only where data quality supports the strategy being tested. Simulation, testnet, and live results will remain distinguishable.

The planned dashboard will report net PnL, drawdown, fees, funding where available, exposure, and execution exceptions. It will not label a configuration profitable or safe based on a single historical result.

## Why TxFlow

TxFlow documents market/account reads, signed trading actions, streaming updates, and agent authorization. Its Builder Code documentation includes applications that route user order flow. Those capabilities make it a relevant integration target for this product. [API reference](https://docs.txflow.com/api/) · [Builder Code](https://docs.txflow.com/getting-started/builder-code)

We are seeking developer onboarding to validate the integration and progress toward a controlled pilot. The intended contribution is a focused user interface for legitimate automated trading, clear performance reporting, and actionable integration feedback. These are product objectives, not proven adoption or volume commitments.

## Execution and user control

The intended architecture separates the web interface from a persistent executor, so closing a browser does not stop monitoring. Users explicitly authorize trading access. Their primary wallet key or seed phrase will never be requested by the application.

Delegated trading credentials still carry material risk: they can authorize trades that lose money. Before a public pilot, the implementation must validate credential protection, account isolation, revocation, risk limits, restart recovery, and the exact permissions exposed by the platform.

## Build sequence

1. Document the proposal and demonstrate the intended user journey.
2. Build read-only views and labelled simulation.
3. Validate supported API actions in test environments.
4. Run a limited, authorized live pilot with reconciled execution records.
5. Invite a small group after operational and account-isolation checks pass.
6. Consider additional strategies and cross-exchange hedging based on evidence and demand.

See [the roadmap](docs/ROADMAP.md) for completion criteria. This sequence is a plan, not a release schedule.

## Repository scope

```text
docs/
  product/          Product, bot behavior, and user experience
  engineering/      Architecture, evaluation, and validation
  BUILDER-APPLICATION.md
  RESEARCH.md
  ROADMAP.md
  archive/          Earlier planning material
integracoes/        Portuguese API research and future hedged-cycle notes
examples/           Non-executable configuration examples
```

The earlier [Portuguese product plan](docs/PLANEJAMENTO-PRODUTO.md) and [integration research](integracoes/README.md) provide background. The English documents linked above define the current MVP. No installation or trading command is provided because executable software has not yet been released.

## Project discussion

Questions and implementation feedback can be raised through this repository's Issues when enabled. Please use [the contribution guide](CONTRIBUTING.md). Never post account credentials, private keys, seed phrases, or signed trading payloads.

**Last reviewed:** 23 October 2026. Platform capabilities and access requirements must be rechecked during implementation.

