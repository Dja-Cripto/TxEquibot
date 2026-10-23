# Evaluation methodology

## Three distinct environments

Historical backtest: evaluate against a recorded dataset. Paper trading: simulate decisions and fills against incoming data. Testnet execution: exercise integration behavior on a test network. None is interchangeable with actual mainnet performance.

The first deliverable may offer simulation and paper trading without historical backtesting if suitable historical data is unavailable. Do not invent missing depth, funding observations, or execution history.

## Reproducibility

Record strategy version, parameters, dataset identity, venue/instrument, time period, timezone, resolution, cost model, execution assumptions, and software version. Retain the run's trade ledger and any excluded periods. A configuration change creates a new version.

Use only information available at each decision time. Separate parameter tuning from out-of-sample evaluation. Keep unsuccessful trials available rather than reporting only the best result. Do not use a score that implies guaranteed suitability.

## Execution assumptions

Model spread, fees, latency, slippage and partial fills at a fidelity supported by available data. A candle touching a limit price does not prove an order would have filled. Ambiguous intra-candle trigger ordering needs a disclosed conservative policy. Missing order-book data limits queue-position and market-impact claims.

Funding depends on actual venue rules, timestamps and available records; present estimates separately. Testnet fills are useful for protocol validation but do not establish mainnet liquidity or profitability.

## Reporting

Include net PnL, realized/unrealized components, maximum drawdown, turnover, fees, funding, sample size, exposure, cycle duration, and exceptions. Identify reporting currency, valuation timestamps, and missing observations.

Reconcile exchange accounting conventions before combining metrics. Do not subtract fees already included in a PnL field. Execution slippage may be reported against a reference price, but not charged twice when already reflected in fill-based PnL. Deposits and withdrawals are capital movements, not strategy profits.

Compare simulations using matching periods, initial capital and cost assumptions. For live comparisons, identify differences in configuration, market data, actual fills and costs instead of describing all differences as strategy performance.

## Release gate

A reproducible small dataset must produce independently reconciled trades and costs. Test missing data, adverse gaps, ambiguous bars, partial fills and boundary timestamps. Reports must visibly label the environment and assumptions before the feature is released.

