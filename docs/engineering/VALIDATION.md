# Validation and release evidence

These are planned acceptance checks. No test has been executed against a trading implementation because none is present.

| Scenario | Required evidence |
|---|---|
| Normal cycle | Entry fills on both venues, positions, exit fills and final balances/positions reconcile |
| Partial entry | Remaining order is tracked; exposure and original deadline stay bounded |
| Second leg rejected or late | No blind retry; filled leg unwound within the unhedged window and slippage limit, or escalated; entries paused |
| Timer anchor | Hold clock starts at confirmed protection of both legs, not at click or first fill |
| Edge gate | Entry refused with recorded inputs when carry < multiple of costs; allowed when it clears; re-checked on every repeat |
| Builder fee | Fee within cap and user-approved is charged and shown; absent, revoked or over-cap approval is detected, not assumed collected |
| Per-venue margin | A move that stresses one leg triggers the early-close rule from that venue's margin health, not from net delta |
| Lost response | Query/reconciliation prevents blind duplicate submission |
| Duplicate/out-of-order stream event | Accounting and position are not counted twice |
| Restart before/after deadline | Original state recovered; expired cycle prioritizes exit |
| Two workers | A stale owner cannot continue to act on a strategy |
| Venue pair outage | One venue unavailable during close: retries bounded, exposure visible, cycle never marked complete |
| Stale data or rate limit | New exposure blocked; backoff respected; incident visible |
| Authorization revoked | Writes stop and open exposure remains visible |
| Partial or failed close | Cycle not marked complete and repeat remains blocked |
| Manual account interference | Unexpected exposure detected and reconciled |
| Account isolation | Another user cannot view data, change settings or issue commands |
| Evaluation accounting | Independent trade/cost calculation matches reported result |
| User controls | Pause, cancel and close have distinct, tested outcomes |
| Secret handling | No credentials in logs, browser storage, reports or repository |
| UI failure state | Stale/missing values cannot appear as healthy/zero |

## Progression

First use deterministic local fixtures and simulated adapters. Then exercise venue test environments where available (TxFlow testnet needs no application; a test environment for the second venue is unconfirmed, and a simulated leg must never be combined with a real one to imitate a hedge). A limited live pilot requires confirmed access, tested authorization, validated limits and recovery, and explicit activation. Invited users additionally require verified account isolation, operational monitoring and a usable incident process.

## Incident behavior

Capture the strategy/account identifiers, last confirmed venue state, unresolved intentions and timestamps without secrets. Block new exposure as appropriate, retain monitoring, reconcile and present the actual state. Never describe an unavailable exit as completed. Record the recovery action and reason before resuming.

## Evidence format

Maintain a release record listing software version, scenarios run, environment, results, known limitations and unresolved defects. A checklist alone is not proof of a passing test. Numerical risk thresholds must be defined and reviewed before execution, not selected silently by the developer.
