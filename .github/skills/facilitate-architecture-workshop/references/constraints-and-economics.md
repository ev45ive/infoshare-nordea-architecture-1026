# Constraints and economics

Read for estimation, technology choice, resource changes, feasibility, and consequences.

## Operating envelope

Record machine counts/specifications, failure domains, storage/network limits,
environments, external dependencies/limits, team skills, person-days, support coverage,
release windows, money, and commitments. Separate hard limits, negotiable targets,
assumptions, and preferences.

Keep technologies open. Require resource and operational fit. Include learning,
configuration, integration, tests, security, deployment, monitoring, upgrades, recovery,
and support. Managed services move responsibility/cost rather than erasing them. New
funding does not instantly create expertise or elapsed time.

## Two clocks

- Workshop time: discussion, exploration, documentation.
- Scenario time: implementation, procurement, operation, incidents, migration.

Advance scenario time only on an accepted action or authorized event. State the interval
and effects. Accrue recurring costs once for the interval. Do not charge fictional work
because participants spent workshop time investigating.

## Economic entries

| View | Include |
| --- | --- |
| Initial investment / CAPEX | Procurement, implementation, learning, migration |
| Recurring OPEX | Hosting, licensing, monitoring, support, reconciliation, upgrades |
| Capacity | Skill/role-specific work, person-days, dependencies, operating headroom |
| Business outcome | Margin/revenue protected, opportunity cost, conversion, fulfillment cost |
| Risk and debt | Exposure, uncertainty, future work/interest, owner, revisit trigger |

Use CAPEX/OPEX as planning views; do not invent formal accounting treatment. Separate
incurred, committed, estimated, optional costs. Revised forecasts retain earlier estimates.
Cancelling work is not automatically a refund. Avoid double-counting salary and person-day
cost in one financial total; disclose any conversion basis.

Record entry ID, linked decision/event, type, amount/unit/currency, interval, status,
source/estimate basis, uncertainty, and owner. Append corrections/recoveries; retain
accepted entries. Derive totals from entries, not improvised revised balances.

## Contextual numbers

- Traffic: operation mix, baseline, peak, interval/duration, payload/concurrency, retries.
- Latency: operation, percentile, window, samples, success/failure inclusion, measurement point.
- Capacity: hardware, workload, dataset, test conditions, headroom, uncertainty.
- SLO: journey/operation, SLI, target, window, exclusions, measurement, owner.
- SLA: agreed scope, contractual source, consequence, amendment authority.
- Business effect: affected segment, baseline, interval, amount/range, evidence/confidence.

Do not confuse QPS with latency percentiles, uptime with completed business work, or a
demand with proven capability. Separate request acceptance, durable recording, and business
completion when relevant. Check state ownership, failures, duplicate delivery, and recovery.
Use CAP with an actual partition and precise consistency/availability definitions, not
as a slogan for every asynchronous trade-off.

## Consequential choices

For each serious option, examine immediate benefit/cost, operational responsibility,
second-order effects, options preserved/closed, reversibility, and who bears the harm.
Use sourced or accepted estimates; mark unknowns. Do not manufacture precise costs or
failure probabilities. Seek evidence when it could materially change the choice.

Separate risk acceptance from an incident occurring. Apply authorized events only when
preconditions hold; preserve benefits of precautions. If requirements conflict, identify
the conflicting subset and propose scope/date/guarantee/resource/authority changes.
Do not force collapse or punish a thoughtful architecture to preserve a storyline.
