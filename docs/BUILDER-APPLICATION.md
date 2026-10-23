# Builder access request

## Project summary

TxEquibot is a proposed web application that helps TxFlow users configure delta-neutral bot cycles (long on one venue, short on another), evaluate whether the funding carry covers fees and slippage, and monitor both legs with an auditable execution record. It is developed independently and is at the specification and interactive-prototype stage.

The initial scope is one strategy family: equal-notional opposite positions on two venues, a hold duration that starts when both legs are confirmed, bounded risk limits, a minimum-edge gate that refuses entry when expected carry does not cover costs, optional repetition, and clear operational controls. TxFlow is the primary venue; the second leg sits behind an adapter. The application is intended for other users after a limited pilot, not only personal use.

## Requested integration capabilities

- Market metadata, price/order-book data and funding information.
- Account balances, positions, margin and open-order information.
- Authorized agent setup, Builder Code approval and signed order/cancellation actions.
- Order and fill updates for reconciliation and reporting.
- Historical data where available, with documented coverage and limits.

The implementation will respect published limits, use shared streams and caching where appropriate, and reconcile ambiguous outcomes before retrying.

## Builder Code intent

The form asks for a builder address that receives Builder Fees, and TxFlow's documentation makes Builder Code the mechanism for apps that route flow. Our position: no fee rate is committed and the pilot default is zero. If a fee is introduced it will stay within TxFlow's cap, be user-approved with the user's main key, and be shown beside the exchange fee in review, in the evaluation (where it is charged against the expected carry) and in reports. We understand that the builder address must hold at least 100 USDC in its perp account for fees to accrue, and that TxFlow ignores an unapproved or over-cap fee without rejecting the order.

## Proposed rollout

Documentation and prototype first; read-only testnet integration and simulation next; then testnet execution including recovery from a rejected second leg; then a limited live pilot after access approval and validation. A small invited group follows only after multi-user isolation and operational controls are verified. No existing users, trading volume or production deployment are claimed.

## Position on volume and Points

TxEquibot is not designed to farm Points or manufacture volume. One account per user, no self-trading, and a minimum-edge gate that refuses cycles that do not pay for themselves. We acknowledge that a hedged cycle places one leg on another venue and do not present it as full volume for TxFlow.

## Builder background

Previous work includes a separate Python prototype using Hibachi API calls and a local web dashboard. Its present operation and public release status have not been verified. This experience informs integration planning; it is not evidence of an existing TxFlow integration. The current prototype reads TxFlow's public testnet endpoints from the browser to show real funding and instrument metadata, and sends no orders.

## Form alignment

Primary category: Trading Bot. Supporting capabilities: Analytics / Dashboard and Portfolio Management, if multiple selections are permitted. Team: Solo Builder. Stage: **Prototype** is now verifiable at the project website (published 23 October 2026); **Idea Stage** remains the conservative alternative. Describe it accurately as a simulated prototype with read-only testnet data. Prior-launch answers must reflect the developer's actual release history, not planned integrations.

APIs expected: Public Market Data, Private Trading API, Order Management, Account Information, WebSocket Streams, Authentication / Signing; Historical Data if available. Use case: arbitrage-style hedged carry and portfolio management, described honestly as bounded delta-neutral cycles.

Expected users and API usage remain estimates to finalize before submission. Use an explicit small-pilot estimate, not a claim of an installed base. Public streams can be shared; private reconciliation and operations add per-user load. Builder Address (an EVM address that receives fees), contact details and any claims about prior launches are the founder's to supply.

## Questions for onboarding

1. Which endpoints, environments and API versions should the project use for mainnet reads and writes?
2. Is automated delta-neutral trading expressly covered, and are there constraints on hedged strategies?
3. What limits apply to a multi-user server sharing an IP?
4. What historical data coverage is available for evaluation, including funding history?
5. Is a spot–perpetual hedge on TxFlow supported or planned, and is the spot API stable?
6. How should a builder fee and the 100 USDC builder-account requirement be handled during a pilot?

This document is prepared for review, not submitted automatically. Individual eligibility does not constitute access approval.
