# TxEquibot — project brief

## Proposal

TxEquibot is a proposed web application for configuring, evaluating, and monitoring trading bots on TxFlow. It is being planned by an independent developer for eventual use by other traders.

The intended workflow is to configure explicit trading rules, evaluate them in a clearly labelled simulation, review costs and risk limits, and then authorize live execution once access and validation requirements are met.

## Initial scope

The first version will focus on one configurable execution strategy with entry conditions, position limits, time-based exits, and controlled repetition. A dashboard will show orders, positions, net performance, and reasons for pauses or exits.

Evaluation will start with simulated or paper trading. Historical backtesting will be added only where suitable data and documented execution assumptions are available. Simulated, testnet, and live results will remain clearly distinguished.

## Integration approach

The proposed integration uses market data, account information, authenticated order management, and real-time streams. Trading authorization will be explicit, credentials will be isolated per user, and interrupted operations will be reconciled before retrying.

## Delivery approach

Documentation and demonstration → test-environment integration → authorized, limited live pilot → small invited user group. Broader strategy support and cross-exchange delta-neutral cycles are later milestones.

## Status

Idea and specification stage. No production-ready TxFlow integration, user base, performance record, or access approval is claimed. Earlier development experience includes a separate Hibachi API prototype and local dashboard, whose present functionality has not been validated.

## Access request

We seek developer access and onboarding guidance to validate the proposed TxFlow integration and build toward a controlled pilot. The goal is to make bot configuration and performance assessment accessible while providing transparent execution records and risk controls.

