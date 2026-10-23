# TxEquibot

### Configure delta-neutral cycles. Evaluate whether the edge pays. Understand every execution.

TxEquibot is a proposed web application for **delta-neutral position cycles with TxFlow as the primary venue**: long on one venue, short on another, with explicit rules, honest cost accounting, and an execution record a user can audit. It is being designed by an independent developer for traders who want to configure hedged bots, evaluate their assumptions in simulation, and monitor execution through one understandable interface.

**Stage:** specification and interactive prototype · **Primary venue:** TxFlow · **Second leg:** adapter-based (Hibachi researched) · **Delivery:** web application with a persistent execution service · **Builder:** individual developer

> This repository contains product and engineering documentation. An interactive prototype with simulated evaluations and optional read-only TxFlow testnet data has been built; it places no orders and connects no wallet. The trading application has not been implemented. TxFlow mainnet access has not been granted. No trading performance or existing user base is claimed.

**Website:** [txequibot.setupdja.website](https://txequibot.setupdja.website/)

A minimal placeholder is currently live at that address. The prototype will replace it when published. Website source is maintained separately and intentionally excluded from this public repository.

## Start here

| Document | What it explains |
|---|---|
| [Product proposal](docs/product/PROPOSAL.md) | User problem, product value, scope, commercial model, and why TxFlow |
| [Bot behavior](docs/product/BOT-BEHAVIOR.md) | How a hedged cycle opens, becomes protected, is monitored, closes, recovers and repeats |
| [User experience](docs/product/USER-EXPERIENCE.md) | Screens and the journey from configuration to monitoring |
| [Website specification](docs/product/WEBSITE.md) | Public site content, visual direction, prototype behavior, delivery criteria |
| [System architecture](docs/engineering/ARCHITECTURE.md) | Executor, venue adapters, persistence, account isolation, Builder Code |
| [Strategy evaluation](docs/engineering/EVALUATION.md) | Simulation method, costs, the minimum-edge gate, metrics, limitations |
| [Validation plan](docs/engineering/VALIDATION.md) | Evidence required before test and live releases |
| [Roadmap](docs/ROADMAP.md) | Milestones, gates, open decisions |
| [Builder access request](docs/BUILDER-APPLICATION.md) | What we request from TxFlow, form answers, onboarding questions |
| [Research and evidence](docs/RESEARCH.md) | Official references, observations, and the line between fact and hypothesis |
| [Integration kit (Portuguese)](integracoes/README.md) | TxFlow and Hibachi API notes, cycle mechanics, checklist |

## The problem we want to solve

A hedged position looks simple and is not. Funding carry has to pay for four fills, a builder fee if any, and slippage. Each venue holds its own margin, so a position that is delta-neutral on paper can still lose a leg to liquidation. A rejected second order leaves a directional position at the worst moment. A timer is not an edge.

Our product hypothesis is that a focused workflow makes these decisions easier and safer for TxFlow users: **configure → evaluate → review → authorize → monitor**, with a bot that refuses to open a cycle whose expected carry does not cover its costs. We will validate that with an internal pilot and a small invited group before expanding.

## What the first version will do

- **Configure explicit rules:** instrument, direction per venue (chosen by the user, never random), bounded size, hold duration, delta tolerance, entry-basis limit, loss limit, repetition and cooldown.
- **Evaluate before execution:** clearly labelled simulation showing funding carry against fees, builder fee and slippage; break-even hold; liquidation distance per leg; a margin stress test; a per-cycle ledger with assumptions listed.
- **Gate on edge:** a minimum-edge gate compares expected funding carry over the hold with round-trip costs, using only rates visible at entry, and refuses entry otherwise.
- **Review the whole configuration:** costs including any builder fee, limits, permissions, and behavior during failures before activation.
- **Operate through supported APIs:** signed order management, streams, and reconciliation of actual fills and positions on both venues.
- **Explain what happened:** order history, the reason for each action, net result, exposure and incidents.
- **Keep controls distinct:** pause new entries, stop after the current cycle, cancel pending orders, and close both legs are four different actions.

Live operation is conditional on access approval, integration validation on testnet, and explicit user activation.

## The strategy: bounded delta-neutral cycles

A cycle opens opposite positions of equal notional on two venues. The hold timer starts only when **both legs are confirmed** within the delta tolerance (`protected_at`), not at click or first fill. At the scheduled close the bot cancels the cycle's orders, reads actual positions, reduces both legs and marks the cycle complete only after reconciliation. Repetition requires a flat account and every entry check, including the edge gate, to pass again.

Five and twelve hours are configurable examples, not defaults to be justified by returns. Delta-neutral does not mean risk-free: basis risk, funding that shrinks or flips, per-venue margin and liquidation, one-sided fills and outages remain. See [bot behavior](docs/product/BOT-BEHAVIOR.md).

## Economics, stated plainly

The only source of expected return in this design is the funding differential between venues. On TxFlow, funding settles on a cycle (default hourly) and is paid between traders, not to the exchange. A single read of TxFlow's public testnet on 23 October 2026 showed a BTC funding rate far smaller than the placeholder values in our early planning; that is one testnet sample and not evidence about mainnet, but it shows why the product must evaluate costs first. A short hold paying fees on four fills can need a larger differential than funding provides, which is why the minimum-edge gate exists and why evaluation reports never imply that time in the market creates profit.

## Why TxFlow, and Builder Code

TxFlow documents public reads, locally signed writes with agent keys, streaming updates, a free testnet, and a **Builder Code**: an app that routes order flow can charge a user-approved fee on each fill, up to 0.1% on perpetuals, additional to exchange fees, approved with the user's main key and revocable. Our application is therefore a Builder Code application. A builder fee is one option under consideration, not a committed scheme; if introduced it will stay within the cap, be user-approved, and be shown beside the exchange fee in review and in every report. [API reference](https://docs.txflow.com/api/) · [Builder Code](https://docs.txflow.com/getting-started/builder-code)

TxFlow's Points documentation says wash trading, artificial volume and multi-account farming earn little or nothing. TxEquibot is not designed to optimise Points: one account per user, no self-trading, no volume for its own sake. The edge gate is part of that stance. [How Points work](https://docs.txflow.com/points/how-points-work)

## Execution and user control

The web interface is separate from a persistent executor, so closing a browser does not stop monitoring. Users explicitly authorize trading access with an agent key. Their primary wallet key or seed phrase will never be requested, and withdrawals or transfers are out of scope.

Delegated credentials still carry material risk: they can place losing trades, and limits inside TxEquibot are software limits, not on-chain guarantees. Before a public pilot the implementation must validate credential protection, account isolation, revocation, risk limits, restart recovery and the exact permissions each venue exposes.

## Build sequence

1. Document the proposal and demonstrate the journey with a labelled prototype (done locally; publication pending).
2. Read-only integration on TxFlow testnet, which needs no application.
3. Versioned evaluation with disclosed assumptions.
4. Signed orders, reconciliation and both-leg failure recovery on test environments.
5. Limited, authorized live pilot with reconciled records, after access approval.
6. Small invited group after isolation and operational checks pass.
7. Additional strategies or venues based on evidence.

See [the roadmap](docs/ROADMAP.md) for completion criteria. This sequence is a plan, not a release schedule.

## Repository scope

```text
docs/
  product/          Product, bot behavior, user experience, website
  engineering/      Architecture, evaluation, validation
  BUILDER-APPLICATION.md
  RESEARCH.md
  ROADMAP.md
  archive/          Earlier planning material
integracoes/        Portuguese API research and cycle mechanics
examples/           Non-executable configuration examples
```

The earlier [Portuguese product plan](docs/PLANEJAMENTO-PRODUTO.md) and [specification](docs/ESPECIFICACAO.md) are background; where they differ from the documents linked above, the English documents define the current scope. No installation or trading command is provided because executable trading software has not been released.

## Project discussion

Questions and implementation feedback can be raised through this repository's Issues when enabled. Please use [the contribution guide](CONTRIBUTING.md). Never post account credentials, private keys, seed phrases, or signed trading payloads.

**Last reviewed:** 23 October 2026. Platform capabilities, hosts and access requirements must be rechecked during implementation.
