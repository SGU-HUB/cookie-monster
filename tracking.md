# Tracking

Use a small ledger in JSON, CSV, a database, or a spreadsheet. The storage format is less important than preserving explicit decisions and an audit trail.

## Task fields

- task label
- short description
- current state: open, in progress, blocked, complete, or closed
- two-path status: complete, exact handoff, or not eligible
- remaining action
- verification reference
- last updated time

## Decision fields

- task label
- Sunday-starting week
- decision: awarded, denied, deferred, or revoked
- decision source
- reason
- decision time

## Weekly total

Count explicit awards for the current week, then subtract explicit revocations tied to that week. Do not count completed tasks that have not received an award decision.

## Hourly pace check

1. Determine the current Sunday–Saturday week in Pacific Time.
2. Read the current week’s explicit decisions.
3. Calculate the net awarded total.
4. Read `weekly_target` from `config.json` and compare the total with the configured pace from Sunday 00:00 through the end of Saturday.
5. If the total is on pace, stay silent.
6. If the total is behind pace, check for a qualifying signal during the prior 24 hours.
7. If none exists, post one short thirst signal in the configured request channel and record it.
8. Otherwise, stay silent.

The check observes and reports. It never awards cookies.
