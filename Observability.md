# Observability

## 3 Concerns:

- Instrumentation - how we colect evidence about system behavior.
- Analysis - How we explain behavior, failures and dependencies.
- Control: How we detect unacceptable behavior and verify architectural guarantees.

## The 7 mechanisms — what tracks what?

| Level | Mechanism              | What it tracks                                                      | Questions it answers                                        |
| ----- | ---------------------- | ------------------------------------------------------------------- | ----------------------------------------------------------- |
| 1     | Logs                   | Individual Event, Error, State transitions                          | What happened? Why did this operation fail?                 |
| 2     | Metrics                | Aggregated measurements, rates, durations, resource usage           | How much? How often? How fast?                              |
| 3     | Disributed trace       | Request execution across services and dependencies                  | Where did time go? Which service failed?                    |
| 4     | Correlation Id         | Relationships between logs, metrics, traces and business operations | Which evidence belongs to the same failure?                 |
| 5     | Alerts                 | Conditions that require investigation or action                     | When should somebody react?                                 |
| 6     | SLOs -> SLA            | Measured service quality against explicit objectives                | Are we meeting our service promises?                        |
| 7     | Cardinality management | Number and dimensions of metric time series                         | Can we maintain observability at scale and reasonable cost? |
| 8     | User Analytics         | User behaviours                                                     | Business questions / metrics?                               |

- Cardinality isn't really a higher level of observability maturity. It's an engineering constraint affecting the cost and scalability of telemetry.
