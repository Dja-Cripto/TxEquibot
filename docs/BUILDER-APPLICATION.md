# Builder access request

## Project summary

TxEquibot is a proposed web application that helps TxFlow users configure rule-based trading bots, evaluate their assumptions in simulation, and monitor execution and net performance. The project is being developed independently and is currently at the documentation and specification stage.

The initial scope is one bounded strategy family with explicit entry/exit rules, time-based position management, optional repetition, and clear operational controls. The application is intended for other users after a limited pilot, not only personal use.

## Requested integration capabilities

- Market metadata, price/order-book data and funding information.
- Account balances, positions, margin and open-order information.
- Authorized agent setup and signed order/cancellation actions.
- Order and fill updates for reconciliation and reporting.
- Historical data where available, with documented coverage and limits.

The implementation will respect published limits, use streams/caching where appropriate, and reconcile ambiguous outcomes before retrying.

## Proposed rollout

Documentation and demonstration first; test integration and simulation next; then a limited live pilot after access approval and validation. A small invited group follows only after multi-user isolation and operational controls are verified. No existing users, trading volume or production deployment are claimed.

## Builder background

Previous work includes a separate Python prototype using Hibachi API calls and a local web dashboard. Its present operation and public release status have not been verified. This experience informs integration planning; it is not evidence of an existing TxFlow integration.

## Form alignment

Primary category: Trading Bot. Supporting capabilities: Analytics / Dashboard and Portfolio Management, if multiple selections are permitted. Team: Solo Builder. Stage: Idea Stage until a functional prototype exists. Prior-launch answers must reflect the developer's actual release history, not planned integrations.

Expected users and API usage remain estimates to finalize before submission. Use an explicit small-pilot estimate, not a claim of an installed base. Public streams can be shared; private reconciliation and operations add per-user load.

## Questions for onboarding

1. Which endpoints, environments and API versions should the project use?
2. Which account/agent and Builder Code setup is required for this use case?
3. What limits apply to a multi-user server sharing an IP?
4. What historical data coverage is available for evaluation?
5. Does the granted access expressly cover the described automated trading use?

This document is prepared for review, not submitted automatically. Individual eligibility does not constitute access approval.
