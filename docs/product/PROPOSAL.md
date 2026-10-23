# Product proposal

## Purpose

Build a focused web application that helps individual TxFlow traders configure delta-neutral bot cycles, assess whether their economics hold, and understand live execution. The project is planned as a solo-built product for eventual use by others, not just a private script.

## User problem and validation

The problem hypothesis is a gap between defining a hedge and understanding its economic and operational consequences. A user may expect funding carry without seeing that four fills, a builder fee if any, and slippage must be paid first; may not realise that each venue holds its own margin; and may not know what the bot does when one leg fails.

Before expanding the scope, observe whether pilot users can explain a cycle's two legs, its maximum configured exposure, why it would refuse to open, and what happens when the second leg is rejected. Record confusion, setup failures and unsupported assumptions. Do not treat competitor features as proof of demand for our implementation.

## Intended value

One versioned configuration connects setup, evaluation and execution records. A user should be able to answer: What did I authorize? What did it cost, including fees I pay to TxFlow and to the app? Why did the bot open or refuse? What happened to each leg? What remains open?

The differentiation hypothesis is a concise, TxFlow-focused experience with a minimum-edge gate, visible assumptions and traceable two-leg execution. Simulation and bot dashboards are established capabilities in competing products; we do not claim exclusivity.

## MVP boundaries

Included: one delta-neutral cycle strategy; TxFlow as primary venue and one second venue behind an adapter; a limited instrument set validated against venue metadata; configuration review; simulated evaluation including break-even hold and margin stress; the minimum-edge gate; positions and order history; explicit operation controls.

Initial constraints: one active cycle per user; dedicated positions for the bot with no concurrent manual trading in the same account/instrument during the pilot; direction chosen by the user; no automatic increase in leverage or allocation; one account per user. Where position isolation cannot be enforced by a venue, detect unexpected activity and suspend new entries pending reconciliation.

Excluded initially: strategy marketplace, copy trading, autonomous AI decisions, martingale, automatic direction selection, more than two venues, mobile/desktop applications, transfers and withdrawals, trading Outcome markets. A future feature must earn its place through validated demand and a separate engineering scope.

## Economics and the minimum-edge gate

Expected return comes only from the funding differential between the venues. It must exceed round-trip costs: exchange fees on four fills, any builder fee on the two TxFlow fills, and slippage. The minimum-edge gate requires expected carry over the configured hold to be at least a configured multiple of those costs, computed from rates visible at entry, and refuses entry otherwise. The gate cannot see future funding; it reduces, and does not remove, the chance of a negative cycle.

A time-based cycle is an operating rule. It is not evidence of an economic benefit, and the product must not present it as one. Evaluation outputs must show a negative or zero outcome when that is what the assumptions imply.

## Fit with TxFlow

TxFlow documents Builder Code for apps that route order flow, public reads, a free testnet, agent keys and hourly funding. TxEquibot is designed to use those mechanisms directly. Its stance on volume is explicit: TxFlow's Points documentation treats wash trading, artificial volume and multi-account farming as non-rewarded. TxEquibot has one account per user, never trades against itself, and refuses cycles that do not pay for themselves. A hedged cycle also sends one of its two legs to another venue; we state that openly rather than present it as full volume for TxFlow.

## Success criteria

Product: users understand configurations, costs and status; setup can be completed without sharing primary wallet secrets; evaluation assumptions are discoverable; the edge gate's reason is understood.

Engineering: confirmed fills on both venues determine positions; ambiguous requests do not create duplicate exposure; a failed second leg is unwound within bounds or escalated; active positions remain monitored when entries pause; restart recovery preserves the original cycle deadline.

Pilot metrics: setup completion, evaluation completion, entries refused by the gate, order rejection rate, one-sided-fill incidents, time to reconcile, data freshness, and gap between estimated and observed costs. Numerical targets are set after measuring a baseline, not invented.

## Commercial model

Undecided. TxFlow's Builder Code is the expected mechanism: a user-approved fee per fill, capped by TxFlow at 0.1% on perpetuals, additional to exchange fees, with the builder address needing at least 100 USDC in its perp account to accrue. A software plan is an alternative. No rate, revenue, volume or user count is committed. Any fee must be disclosed in configuration review, in the evaluation (where it is charged against the carry) and in performance reporting. Pilot default is no fee.

## Later expansion

Additional strategies and venues, based on evidence. A TxFlow-native hedge, such as spot against perpetual on one venue, is a candidate if the spot API is documented and stable; TxFlow currently marks its spot instrument standard as unstable. Hibachi is the researched second connector; the application's value does not depend on that choice alone.
