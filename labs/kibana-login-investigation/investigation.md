# Findings from Simulated Authentication Events

## Evidence

The supplied dataset contains 680 events: 183 failures and 497 successes. All failures are included in the tables below.

| Account | Failed logins |
| --- | ---: |
| alex | 104 |
| sam | 23 |
| morgan | 20 |
| taylor | 20 |
| jordan | 16 |

| Source IP | Failed logins |
| --- | ---: |
| 203.0.113.50 | 80 |
| 192.0.2.10 | 41 |
| 198.51.100.15 | 35 |
| 192.0.2.20 | 27 |

All 80 events from `203.0.113.50` target `alex` and fail. Sorted timestamps are two seconds apart, covering 158 seconds from the first event to the last on October 16, 2026, 16:51:33.566766–16:54:11.566766 UTC.

## Assessment

The repeated failures against one account from one source, at a regular cadence, are consistent with automated password guessing. The synthetic data was constructed for learning this pattern. Failed attempts alone do not prove a successful intrusion, and there are no successful events from this source in the supplied dataset.

Other successful logins for `alex` require context before they can be considered suspicious. This lab does not include device reputation, MFA results, identity-provider records, or endpoint evidence.

## Follow-up in a real investigation

- Review successful logins before and after the burst, including device and session context.
- Check whether the source targeted other accounts or appeared in other log sources.
- Review MFA, account lockout, and identity-provider alerts.
- Escalate according to the organization's incident process and evaluate appropriate access controls with the responsible team.

These are proposed investigation steps; no production containment actions were performed.
