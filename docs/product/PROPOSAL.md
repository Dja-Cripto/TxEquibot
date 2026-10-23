# Product proposal

## Purpose

Build a focused web application that helps individual TxFlow traders configure rule-based bots, assess their behavior, and understand live execution. The project is planned as a solo-built product for eventual use by others, not just a private script.

## User problem and validation

The problem hypothesis is a gap between defining rules and understanding their economic and operational consequences. A user may see attractive historical PnL without understanding costs, drawdowns, incomplete fills, or how a bot behaves during an outage.

Before expanding the scope, observe whether pilot users can explain a bot's entry, exit, maximum configured exposure, and pause behavior after reviewing the proposed interface. Record confusion, setup failures, and unsupported assumptions. Do not treat competitor features as proof of demand for our implementation.

## Intended value

One versioned configuration connects setup, evaluation, and execution records. A user should be able to answer: What did I authorize? What happened? Which costs were included? Why did the bot stop? What remains open?

The differentiation hypothesis is a concise, TxFlow-focused experience with clear assumptions and traceable execution. Simulation and bot dashboards are established capabilities in competing products; we do not claim exclusivity.

## MVP boundaries

Included: one rule-based cycle strategy, a limited instrument set validated against venue metadata, configuration review, simulated evaluation, positions and order history, and explicit operation controls.

Initial constraints: one active strategy per user, no simultaneous manual trading in the same account/instrument during the pilot, and no automatic increase in leverage or allocation. Where account isolation cannot be enforced by the venue, detect unexpected activity and suspend new entries pending reconciliation.

Excluded initially: strategy marketplace, copy trading, autonomous AI decisions, martingale, multi-exchange execution, mobile/desktop applications, transfers, and withdrawals. A future feature must earn its place through validated demand and a separate engineering scope.

## Success criteria

Product: users understand configurations and operational status; setup can be completed without sharing primary wallet secrets; simulation assumptions are discoverable.

Engineering: confirmed fills determine positions; ambiguous requests do not create duplicate exposure; active positions remain monitored when entries pause; restart recovery preserves the original cycle deadline.

Pilot metrics: setup completion, evaluation completion, order rejection rate, time to reconcile, data freshness, and gap between estimated and observed costs. Establish numerical targets after measuring a baseline, rather than inventing results.

## Commercial model

Undecided. A software plan or explicitly approved Builder Code fee may be evaluated later. Fees, if introduced, must be disclosed in configuration review and performance reporting. No fee rate, revenue, volume, or launch user count is committed at this stage.

## Future hedged execution

The original concept includes opposite positions across two venues and repeating 5-hour or 12-hour cycles. It remains a future module. Hibachi has been researched as a possible second connector; the initial application does not depend on that connector. Hedged execution requires independent margin monitoring and a policy for one-sided fills.

