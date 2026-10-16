# Cookie System

A lightweight accountability system for completing useful work without self-awarding credit.

## Core goal

- Aim for the configured cookie target during each **Monday–Sunday PT week**. The `weekly_target` setting defaults to **10**.
- One task can earn at most **one cookie**.
- A task is eligible only through the [two-path standard](two-path-standard.md).
- The human reviewer makes every final award, denial, and take-back decision.
- The tracker records decisions; it does not make them.

## Documentation

- [Rules](rules.md)
- [Agent skill](SKILL.md)
- [Two-path standard](two-path-standard.md)
- [Awarding](awarding.md)
- [Tracking](tracking.md)
- [Weekly ritual](weekly-ritual.md)
- [Setup](setup.md)

## Automation

An hourly check reads `weekly_target` from [`config.json`](config.json), then compares explicitly awarded cookies with the pace required to reach that target by the end of Sunday. If the total is at risk, the system may post one short thirst signal in the configured request channel asking for a concrete project. It must remain silent when on pace and must not spam.

Suggested signal:

> I’m behind pace for {weekly_target} cookies this week. Send me one concrete project I can finish to earn one.

## Principle

Useful completion beats activity. Short, specific blocker reports count when they tell the reviewer exactly what action is required. Jargon walls that do not move a task forward earn nothing.
