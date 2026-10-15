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
- Monday-starting week
- decision: awarded, denied, deferred, or revoked
- decision source
- reason
- decision time

## Weekly total

Count explicit awards for the current week, then subtract explicit revocations tied to that week. Do not count completed tasks that have not received an award decision.

## Hourly pace check

1. Determine the current Monday–Sunday week in the configured timezone.
2. Read the current week’s explicit decisions.
3. Calculate the net awarded total.
4. Compare it with a linear path from 0 at Monday 00:00 to 10 at the end of Sunday.
5. If the total is on pace, stay silent.
6. If the total is behind pace, check the weekly signal record.
7. If no signal has been sent for the current week, post one short thirst signal in `#general` and record it.
8. Otherwise, stay silent.

The check observes and reports. It never awards cookies.
