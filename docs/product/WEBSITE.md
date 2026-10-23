# Website specification

Public address: [txequibot.setupdja.website](https://txequibot.setupdja.website/).

Status as of 23 October 2026: a white placeholder displaying “TxEquibot” is online. This document defines the next implementation; it does not claim those features already exist.

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

Suggested headline: **Configure a trading bot. Evaluate its assumptions. Understand its execution.**

Supporting text: **TxEquibot is being developed to help TxFlow traders configure rule-based automation, explore simulated behavior, and monitor execution through a clear web interface.**

Visible status: **In development.** Primary link: **Read the project proposal**, pointing to the repository. Add **Explore the demo** only when the demonstration exists, with its simulated status visible.

### How it works

Five concise steps: Configure → Evaluate → Review → Authorize → Monitor. Explain that the trading stages describe the intended product and are not yet available. Configuration includes explicit entry/exit rules; evaluation includes costs and assumptions; monitoring shows actual position and order state when integration is ready.

### Planned capabilities

Three groups: rule-based trading bots, transparent evaluation, and execution monitoring. Limit the page to the initial TxFlow scope. Cross-exchange delta-neutral cycles may appear under future development, clearly separate from current delivery.

Do not claim a timer creates profitability. A single-venue long or short bot is directional, not delta neutral.

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

Build a clean, professional, light-first presentation consistent with the current white placeholder. Use generous spacing, dark readable text, a restrained accent color, and clear typography. The future dashboard may offer a dark theme, but marketing and application should share typography and components.

Avoid clutter, animated profit counters, aggressive financial imagery and excessive effects. Support desktop and mobile, keyboard navigation, visible focus, adequate contrast and reduced-motion preferences. No horizontal overflow at narrow phone widths.

Primary copy should be English for the developer-program review. Portuguese can be added as a complete, consistent alternative later; avoid mixed-language sentences.

## Demonstration behavior

The user selects a simulated instrument, direction, size and holding period, then reviews a simulated configuration and opens a sample evaluation. A monitoring screen shows a mock cycle and the distinct controls for pausing new entries, stopping after a cycle and requesting closure.

Display a persistent simulated-data label. Do not connect mock buttons to real APIs. Do not collect wallet secrets or imply that a static report was computed from newly entered values. If the report is illustrative, label it as a fixed example; if interactive, implement the corresponding calculation.

## Future live application requirements

Authenticate account ownership, authorize an agent separately, validate parameters server-side and require explicit activation. Keep the executor independent of the browser. Present environment, stale data, residual exposure and incidents accurately. Follow the architecture, bot behavior and validation documents before enabling trading.

## Source and publication policy

Local website source belongs in the workspace's `site/` folder. That folder is excluded through `.gitignore` and must not be committed or pushed to the public documentation repository. Public GitHub may contain the website URL and this specification.

The current site is served on the owner's VPS through Cloudflare Tunnel. Infrastructure secrets and access details belong outside public documentation. Publishing a documentation change does not automatically deploy the website; they are separate workflows.

This document does not authorize expanding the current placeholder by itself. Implement subsequent stages when requested by the project owner.

## Acceptance criteria for the presentation release

- The URL loads through HTTPS and layout works on mobile and desktop.
- The product, audience and current stage are clear without reading GitHub first.
- Navigation and links have implemented destinations; no false functionality.
- Demonstration values and unavailable trading features are labelled honestly.
- Claims match the current GitHub proposal and release status.
- Website source and infrastructure secrets remain outside the public repository.
- Public content has been reviewed for keyboard accessibility, readability and overflow.
