# Website specification

Public address: [txequibot.setupdja.website](https://txequibot.setupdja.website/).

Status as of 23 October 2026: the presentation site with the interactive prototype (stages 2 and 3 below) is live at that address, replacing the earlier white placeholder. The trading application (stage 4) does not exist. This document defines the site's content and rules; it does not claim features that are not live.

## Purpose

Help prospective users and developer-program reviewers understand the product, its initial scope, and its development stage. The website should complement the GitHub documentation with a clear presentation and, in a later step, an interactive demonstration.

The first impression should answer: what is TxEquibot, who is it for, how will it work, and what can be tried today?

## Delivery stages

1. **Current placeholder:** project name on a white page. No forms, wallet connection, or trading.
2. **Product presentation:** explain the proposed product, connect to the GitHub documentation, and identify planned capabilities.
3. **Interactive demonstration:** simulated configuration, evaluation, and monitoring screens. No wallet signature or deposit is needed to explore it.
4. **Trading application:** only after supported integrations, authorization and validation gates are completed. Account connection and execution must be implemented separately from marketing pages.

Do not display working-looking activation or wallet buttons before their behavior is implemented. Until a demo exists, use a documentation link instead of an inactive “Try demo” button.

## Public homepage structure

### Header

Project name and navigation to How it works, Planned features, Roadmap, and GitHub. The brand is TxEquibot; do not imply official TxFlow ownership or partnership.

### Opening section

Headline: **Delta-neutral cycles. Configured, evaluated, explained.**

Supporting text: **TxEquibot is being built to let traders run hedged position cycles — long on one venue, short on another — with explicit rules, honest cost accounting, and an execution record you can audit. TxFlow is the primary venue; other venues connect through a common adapter.**

Visible status: **In development**, with chips for stage, live trading not available, mainnet access not confirmed, evaluations simulated, and market inputs read-only from TxFlow testnet. Primary links: **Open the prototype** (an in-page anchor to the working prototype) and **Read the documentation** (the repository).

### How it works

Five concise steps: Configure → Evaluate → Review → Authorize → Monitor. Explain that the trading stages describe the intended product and are not yet available. Configuration includes explicit entry/exit rules; evaluation includes costs and assumptions; monitoring shows actual position and order state when integration is ready.

### Planned capabilities

Three groups: explicit hedged-cycle configuration, transparent evaluation with a minimum-edge gate, and two-leg execution monitoring. A dedicated **Built for TxFlow** section ties design choices to TxFlow's documentation (agent keys, Builder Code and its visible fee sum, hourly funding, instrument metadata, testnet-first, shared rate limits) with links to the source pages, shows a read-only live testnet table, and states the anti-farming stance.

Do not claim a timer creates profitability. A single-venue long or short position is directional, not delta neutral. Do not present the hedge as full volume for TxFlow: one leg is on another venue.

### Product preview

Once built, show Create bot, Evaluation, and Bot details. Every preview with financial values must say **Simulated example**. Do not use fabricated testimonials, adoption figures, trading volume, returns, or approval badges.

### Development roadmap

Show documentation, demonstration, test integration, controlled live pilot, and invited users. Use honest statuses, not invented launch dates. Link to the complete GitHub roadmap.

### FAQ

Answer: Is live trading available? Is this an official TxFlow product? What does simulation mean? How will trading access be authorized? Does a simulated result predict returns? Each answer must reflect the actual release status.

Initial answers: live trading is not available; TxEquibot is an independent proposed integration; simulations are demonstrations/evaluations with explicit assumptions; future trading requires separate user authorization; simulated results do not predict or guarantee returns.

### Footer

GitHub link, project stage, and independent-project identification. Add contact or policy links only when real destinations and applicable documents exist. Do not invent an organization, support address, or legal entity.

## Visual direction

Build a clean, professional dark presentation with a green accent in the general style of the TxFlow brand: black background, neon green, square corners, hairline borders, bracketed uppercase labels. Marketing and prototype share typography and components. This is a stylistic echo only: do not use TxFlow's logo, imagery or copy, and keep the independent-project statement in the header area, the product section and the footer. The brand is TxEquibot.

Avoid clutter, animated profit counters, aggressive financial imagery and excessive effects. Support desktop and mobile, keyboard navigation, visible focus, adequate contrast and reduced-motion preferences. No horizontal overflow at narrow phone widths.

Primary copy should be English for the developer-program review. Portuguese can be added as a complete, consistent alternative later; avoid mixed-language sentences.

## Demonstration behavior

The user configures a two-venue cycle (instrument, direction, size, hold, limits, edge gate, builder fee, assumptions), sees a live computed summary, runs a seeded and reproducible evaluation computed from the entered values, reads a pre-trade checklist, and watches a simulated executor with distinct controls (pause new entries, stop after the cycle, cancel pending orders, close both legs) and injectable failures (rejected second leg, stale prices, executor restart, price shock, venue outage). Evaluations can be saved as versions and exported.

Display a persistent simulated-data label. The only network use permitted in the prototype is an optional, user-triggered read of TxFlow's public testnet `/info` endpoint for venue-A price, lot and funding; such values must be labelled with source and time, shown as unavailable on failure (never zero), and never mixed silently with placeholders. Do not connect any button to an account-level or signing API. Do not collect wallet secrets. Every evaluation is computed from the entered values; if it ever becomes illustrative, label it as a fixed example.

## Future live application requirements

Authenticate account ownership, authorize an agent separately, validate parameters server-side and require explicit activation. Keep the executor independent of the browser. Present environment, stale data, residual exposure and incidents accurately. Follow the architecture, bot behavior and validation documents before enabling trading.

## Source and publication policy

Local website source belongs in the workspace's `site/` folder. That folder is excluded through `.gitignore` and must not be committed or pushed to the public documentation repository. Public GitHub may contain the website URL and this specification.

The current site is served on the owner's VPS through Cloudflare Tunnel. Infrastructure secrets and access details belong outside public documentation. Publishing a documentation change does not automatically deploy the website; they are separate workflows.

The prototype replaced the placeholder on 23 October 2026. Source stays local and unpublished in this repository.

## Acceptance criteria for the presentation release

- The URL loads through HTTPS and layout works on mobile and desktop.
- The product, audience and current stage are clear without reading GitHub first.
- Navigation and links have implemented destinations; no false functionality.
- Demonstration values and unavailable trading features are labelled honestly.
- Claims match the current GitHub proposal and release status.
- Website source and infrastructure secrets remain outside the public repository.
- Public content has been reviewed for keyboard accessibility, readability and overflow.
