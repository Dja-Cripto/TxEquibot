# Planned user experience

No screens have been implemented. This document specifies the future prototype and product flow.

## Design direction

A restrained financial interface with clear typography, strong spacing, readable tables, and a compact set of high-priority metrics. A dark theme is proposed; color must not be the only indicator of profit, risk, or connection state. Desktop supports configuration; mobile supports monitoring and essential controls.

## Core screens

| Screen | Primary task | Required information |
|---|---|---|
| My bots | Understand current activity | Environment, state, open exposure, data freshness, active incidents |
| Create bot | Define an explicit configuration | Entry/exit rules, size, duration, repetition, limits |
| Evaluation | Understand a simulated result | Version, source/coverage, assumptions, costs, drawdown, trades |
| Review and activate | Authorize the intended behavior | Account, configuration summary, permissions, fees, stop behavior |
| Bot details | Monitor and control | Real positions, pending orders, actions/reasons, deadline, performance |
| Connection | Understand account permissions | Wallet, agent status, environment, authorization and revocation steps |

## User journey

Explore a labelled demonstration → configure a draft → evaluate → inspect assumptions → connect/authenticate → authorize trading if required → review final configuration → activate → monitor.

Connecting a wallet does not start trading. A successful login is not an agent approval. A simulation is not testnet execution, and neither is live performance.

## Essential interaction rules

- The environment label stays visible during configuration and execution.
- Activation requires a valid configuration and explicit user action.
- Missing or delayed values are shown as unavailable/stale, never as zero.
- A paused bot with an open position continues to display that exposure prominently.
- Financial amounts show currency, unit, and estimated/confirmed status.
- Changing live parameters requires a versioned update and clear explanation of its effect on the active cycle.
- A close request remains pending until reconciled; the interface never celebrates an unconfirmed fill.
- Keyboard navigation, focus visibility, contrast, and small-screen layouts are acceptance requirements.

## Future demonstration scope

The proposed prototype will demonstrate Create bot, Evaluation, and Bot details using explicitly simulated data. It should help a reviewer understand the intended product without a deposit or wallet signature. Building this prototype is a later task; this repository currently contains documentation only.

