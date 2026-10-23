# Research and evidence

Reviewed 23 October 2026. Sources are selected for relevance, not as a verified market-share ranking. Feature descriptions reflect published documentation and read-only requests to public endpoints, not hands-on trading tests.

## TxFlow sources

| Source | Observed information | Design implication |
|---|---|---|
| [TxFlow application](https://txflow.com/apply) | Builder Code early-access form (embedded Google Form): project, API needs, contact, and a builder address that receives fees | Answer honestly; the application is a Builder Code application |
| [API overview](https://docs.txflow.com/api/) | Hosts `rpc.txflow.com` (mainnet) and `rpc.txflow-testnet.xyz` (testnet); chain IDs 869 / 2511; `x-api-version: 2026-08-16`; reads unauthenticated; writes signed by wallet (setup) or agent key (trading); account setup order: deposit, builder approval, agent approval | Separate data, authorization and execution; testnet first |
| [Builder Code](https://docs.txflow.com/getting-started/builder-code) | Fee in tenths of a basis point; cap 0.1% perpetuals, 1% outcome markets; additional to exchange fees; user approves a cap with the main key (up to 20 builders, revocable); an absent, unapproved or over-cap fee is silently ignored; builder needs at least 100 USDC in its perp account to accrue; mainnet is in a limited-access phase, testnet needs no application | Builder fee is a possible commercial mechanism; show fee sums; never assume a fee was collected |
| [Funding](https://docs.txflow.com/trade/funding) | Funding settles on a cycle (default hourly), paid between traders; rate published by the oracle and readable from `activeAssetCtx`, expressed in percent | Carry is the only source of expected return; read it from the venue |
| [How Points work](https://docs.txflow.com/points/how-points-work) | Points reward genuine perpetual trading; wash trading, artificial volume and multi-account farming earn fewer or no Points; spot and prediction markets earn none in Season 1 | Do not design for Points; one account per user; refuse cycles that do not pay |
| [Rate limits](https://docs.txflow.com/api/rate-limits) | Per-IP limits on `/info`, `/exchange` and WebSocket connections | Share streams, aggregate limits across users |
| [Vaults](https://docs.txflow.com/trade/vaults) | Protocol and user vaults; user-vault creation limited to a pilot group in the early mainnet phase | Out of scope; possible future packaging of a strategy |
| [TIP 1: Spot](https://docs.txflow.com/tip/spot) | Spot instrument standard, marked unstable | A TxFlow-native spot–perpetual hedge depends on a documented, stable spot API |
| [Connect your coding agent](https://docs.txflow.com/api/ai-agents) | Docs published as Markdown for coding agents (`llms.txt`) | Use the Markdown reference when implementing the adapter |

## Observations from public testnet reads (23 October 2026)

Read-only requests from a browser to `https://rpc.txflow-testnet.xyz/info` (`perpMeta`, `activeAssetCtx`, `l2Book`) returned data without credentials. A single sample showed BTC-USDC with a funding value of about 0.0005 (percent per interval, per the documented unit), 50x maximum leverage and a 0.0001 base precision. This is one testnet sample at one moment; it is not evidence about mainnet funding, liquidity or fees, but it is far below the placeholder funding values used in early planning, which is why the product evaluates costs before execution.

## Other references

| Source | Observed information | Design implication |
|---|---|---|
| [MyLiquidBot documentation](https://myliquidbot.com/docs?lang=en) | Publishes TxFlow connection instructions and bot/evaluation capabilities | A useful reference for onboarding and coherent reporting |
| [3Commas backtesting](https://help.3commas.io/en/articles/4829733-dca-bots-backtesting) | Configurations can be evaluated against historical periods | Preserve configuration and evaluation provenance |
| [Cryptohopper evaluation](https://www.cryptohopper.com/blog/how-does-backtesting-work-11207) | Distinguishes historical and forward evaluation | Label data and evaluation mode explicitly |
| [Hummingbot Dashboard](https://hummingbot.org/dashboard/) | Strategy management pattern; legacy dashboard no longer actively maintained | Learn from workflow without assuming that component is a maintained dependency |

## Confirmed context supplied by the founder

A support reply supplied in this conversation states that individual developers and idea-stage projects may apply without an established company or working prototype. Selection remains subject to engineering review. The private ticket image is not published in this repository.

## Claims we are not making

- No public approval-probability model or ranking of preferred bot categories was found. Our reading of what TxFlow values (flow routed through Builder Code, genuine trading, documented developer tooling) is an inference from its documentation, not a published selection criterion.
- MyLiquidBot's own TxFlow documentation does not establish a publicly confirmed bilateral partnership or prove the project's specific authorization terms.
- Competitor features do not prove unmet demand for TxEquibot.
- A backtest, testnet read, simulation or proposed roadmap is not live performance evidence.
- A confirmed mainnet host does not mean TxEquibot has mainnet access, which remains subject to approval.
- This repository does not demonstrate that TxEquibot has received any access from TxFlow or Hibachi.

The product recommendation is an inference: a narrow, explainable workflow with an explicit edge gate and validation gates is easier to assess and deliver as a solo project. It is not a selection criterion attributed to TxFlow.
