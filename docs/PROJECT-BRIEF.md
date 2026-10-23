# TxEquibot — project brief

## Proposal

TxEquibot is a proposed web application for configuring, evaluating and monitoring delta-neutral bot cycles with TxFlow as the primary venue. It is being planned by an independent developer for eventual use by other traders.

The workflow is to configure explicit hedged-cycle rules, evaluate them in a clearly labelled simulation that charges every cost against the expected funding carry, review limits and permissions, and then authorize live execution once access and validation requirements are met.

## Initial scope

One configurable strategy: two opposite positions of equal notional on two venues, a hold duration that starts when both legs are confirmed, bounded risk limits, a minimum-edge gate, and controlled repetition. TxFlow is the primary venue; the second leg sits behind a venue adapter (Hibachi is the researched candidate). A dashboard shows both legs, net delta, margin per venue, the cycle clock, orders, and the reason for every pause or exit.

Evaluation starts with simulation. Historical backtesting is added only where suitable data and documented execution assumptions exist. Simulated, testnet and live results stay clearly distinguished.

## Integration approach

The integration uses public market data, account information, signed order management and real-time streams. Trading authorization is explicit with a delegated agent key, credentials are isolated per user, and interrupted operations are reconciled before retrying. TxFlow's Builder Code is the expected commercial mechanism; no fee rate is committed.

## Delivery approach

Documentation and prototype → TxFlow testnet read-only integration → evaluation → testnet execution including one-sided-fill recovery → authorized limited live pilot → small invited group. More strategies and venues are later milestones.

## Status

Specification plus an interactive prototype (simulated evaluations, optional read-only testnet data, no orders, no wallet). No production TxFlow integration, user base, performance record or access approval is claimed. Earlier development experience includes a separate Hibachi API prototype and local dashboard, whose present functionality has not been validated.

## Access request

We seek developer access and onboarding guidance to validate the integration and build toward a controlled pilot: bot configuration and performance assessment made accessible, with transparent execution records, disclosed fees and risk controls. The application is made through TxFlow's Builder Code early-access form.
