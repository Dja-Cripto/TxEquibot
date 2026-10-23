> Historical planning snapshot. The root README and linked English documents define the current product scope.

# TxEquibot

Web application for configuring, evaluating, and monitoring trading bots on TxFlow. Currently at the idea and specification stage.

**Current product direction:** [Project brief](../PROJECT-BRIEF.md) and [research-based product plan (Portuguese)](../PLANEJAMENTO-PRODUTO.md). The initial release focuses on TxFlow trading automation and transparent strategy evaluation. The cross-exchange specifications below describe a later expansion, not the initial release scope.

See [the product and implementation specification (Portuguese)](../ESPECIFICACAO.md) for the proposed experience, architecture, development stages, and acceptance criteria.

See the [integration kit (Portuguese)](../../integracoes/README.md) for researched API references, authentication, streams, and the proposed repeating 5-hour or 12-hour hedged-position cycles.

## Project status

Planning and specification. This repository currently contains project documentation, not an implemented trading system. TxFlow mainnet API access and express permission for automated trading have not yet been confirmed. Hibachi is the intended second platform. A separate earlier Python project contains Hibachi API integration code and a local web dashboard; its current functionality and release status have not been verified. Cross-exchange delta-neutral execution is planned, not implemented.

## Overview

We plan to build a trading bot that coordinates offsetting positions between TxFlow and a second trading platform. The objective is to maintain a defined net directional exposure while monitoring each platform's positions, margin, execution status, and trading costs.

The proposed product combines automated trading with portfolio management and an analytics dashboard. The initial strategy will be specified before implementation; potential applications include funding-rate differentials and cross-exchange price spreads, subject to execution costs and platform permissions.

Delta neutrality is a target exposure, not a guarantee of profit or protection from liquidation. Each platform maintains its own margin and liquidation rules.

## Planned capabilities

- Coordinate entry and exit of offsetting positions on two platforms.
- Track combined net delta and detect deviations from user-defined limits.
- Monitor margin and liquidation proximity independently on each platform.
- Track funding payments, realized and unrealized PnL, and trading fees, with estimated execution costs reported separately.
- Reconcile submitted orders against confirmed fills and open positions.
- Handle partial fills, rejected orders, stale market data, and connection failures.
- Support configurable position limits, exposure thresholds, and emergency stop procedures.
- Present positions, execution history, exposure, and net performance in a dashboard.

These are planned capabilities; none are represented as currently available.

## Proposed TxFlow API integration

The integration is expected to use public market data, account and position information, authenticated trading actions, order management, and WebSocket updates. Historical information will support reconciliation and performance reporting where available.

The design will use TxFlow's supported API and signing mechanisms. Dedicated agent keys are intended for trading, with account-owner authorization handled separately. Key permissions and storage requirements will be verified during implementation.

Streaming updates, cached market metadata, bounded retries, and request throttling will be used to respect published API limits. Ambiguous order outcomes must be reconciled before retrying an operation that could duplicate exposure.

## Execution and risk design

Orders on two independent platforms cannot be assumed to execute atomically. The implementation must define how much temporary unhedged exposure is acceptable and what happens if only one leg executes.

Before live trading, the specification will define:

1. Supported instruments and how their contract sizes map to comparable exposure.
2. Entry and exit conditions after fees, funding assumptions, and slippage.
3. Maximum position size, leverage, and temporary unhedged exposure.
4. Partial-fill handling, hedge timeouts, and recovery procedures.
5. Margin thresholds and independent liquidation monitoring.
6. Safe behavior during stale data, outages, or loss of connectivity.
7. Emergency stop behavior, distinguishing cancellation of open orders from closing existing positions.

The bot is intended for genuine trading and hedging. Artificial volume, self-trading intended to manufacture activity, spoofing, and other prohibited market practices are outside the project scope. Any incentive information, if later included, would be supplementary to economic performance reporting.

## Development plan

1. Confirm the second platform, strategy, initial users, and API permissions.
2. Specify execution rules and risk limits.
3. Implement read-only market and account monitoring.
4. Build and validate order execution and recovery in test environments, subject to applicable permissions.
5. Add portfolio monitoring and performance reporting.
6. Seek or confirm express written authorization before automated live operation on TxFlow.
7. Begin a limited live pilot only after access approval and validation of risk controls.

## Decisions still open

- Public repository and website URL.
- Second platform and initial instruments.
- Funding differential strategy, price-spread strategy, or both.
- Personal-use pilot versus a product for additional users.
- Team details, initial user estimate, and expected API request volume.
- Any business model or use of Builder Code fees.

## Official references

- [TxFlow builder application](https://txflow.com/apply)
- [Builder API reference](https://docs.txflow.com/api/)
- [SDK documentation](https://docs.txflow.com/api/sdk)
- [API rate limits](https://docs.txflow.com/api/rate-limits)
- [Builder Code](https://docs.txflow.com/getting-started/builder-code)
- [Terms of Use](https://txflow.com/terms)

Platform requirements and parameters may change and must be checked before implementation and deployment.


