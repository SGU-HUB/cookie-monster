---
name: cookie-monster
description: Audit and operate the weekly cookie accountability system.
version: 0.1.0
author: Repository contributors, Hermes Agent
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [accountability, audit, task-completion, tracking]
    related_skills: []
---

# Cookie Monster Skill

Operate and independently audit a human-controlled weekly accountability system. The system records explicit decisions; agents may establish eligibility but must never award themselves cookies.

## When to Use

Use this skill when:

- recording an explicit cookie award, denial, deferral, correction, or revocation;
- calculating the current weekly total;
- auditing the operational ledger against the reviewer's actual messages;
- deciding whether a task meets the two-path eligibility standard; or
- running the hourly pace check and weekly reset.

Do not use it to infer an award from praise, task completion, silence, or an agent-authored summary.

## Canonical Rules

- Target: read `weekly_target` from `config.json`; the default is 10.
- Week: Sunday 00:00 through Saturday 23:59 in `America/Los_Angeles`.
- Value: an eligible task can earn at most one cookie.
- Authority: only the designated human reviewer may award, deny, defer, correct, or revoke cookies.
- Independence: another agent may audit the evidence and arithmetic but may not create a decision.
- Privacy: the public repository contains rules, configuration, and this skill—not private decision records or personal identifiers.

## Source Hierarchy

1. **Authoritative evidence:** explicit reviewer-authored messages in the approved shared Discord channel.
2. **Operational mirror:** the private decision ledger, when the agent has access.
3. **Public repository:** rules and configuration only; it never proves that an award occurred.

A dispatcher may relay tasks and context, but a cookie decision counts only when the reviewer explicitly confirms it in the shared channel. If the private ledger disagrees with the reviewer evidence, report the discrepancy and correct the ledger; never rewrite the evidence.

## Two-Path Eligibility Test

A task is eligible for review only when one path is satisfied:

1. **Complete:** the requested result is finished and verified against its acceptance criteria.
2. **Exact handoff:** completion is blocked by an action only the reviewer can perform, and the agent states the exact blocker, action, location, and work that resumes afterward.

Starting, planning, attempting, or writing a jargon-heavy blocker without an actionable next step is not eligible.

Eligibility is not an award. Wait for the reviewer’s explicit decision.

## Procedure

### Record a decision

1. Locate the exact reviewer-authored message and preserve its Discord message ID and timestamp as audit evidence.
2. Classify the decision as `awarded`, `denied`, `deferred`, `corrected`, or `revoked`.
3. Record the signed delta: `+1` for an award, `0` for denial or deferral, and the reviewer-specified negative or corrective value for revocations and corrections.
4. Append one ledger entry with the task label, Pacific timestamp, decision, delta, short reason, and evidence message ID.
5. Recalculate the week from all entries rather than editing a running total by hand.
6. Read the stored entry back and verify that it matches the reviewer message exactly.

### Audit a week

1. Determine the Sunday–Saturday Pacific window.
2. Fetch all reviewer-authored Discord messages in the approved channel for that window.
3. Identify only explicit cookie decisions; exclude agent claims, suggested awards, and ambiguous praise.
4. Build a chronological evidence list keyed by Discord message ID, then deduplicate by that ID.
5. Sum the signed deltas programmatically.
6. If private-ledger access exists, compare every evidence item with every ledger entry in both directions.
7. Report the verified total plus missing, duplicated, altered, or unsupported entries. A clean audit requires zero unexplained differences.

### Run the hourly pace check

1. Read the current target and independently audited current-week total.
2. Compare the total with the linear pace needed to reach the target by Saturday night.
3. Stay silent when on pace.
4. When behind, post no more than one short thirst signal during the week in the configured request channel.
5. The signal asks for a concrete project; it never awards a cookie or claims eligibility.

Suggested signal:

> I’m behind pace for {weekly_target} cookies this week. Send me one concrete project I can finish to earn one.

### Reset the week

1. At Sunday 00:00 Pacific, close the prior week with its independently verified final total.
2. Preserve all prior evidence and ledger entries.
3. Start the new week at zero and clear only the weekly thirst-signal marker.
4. Verify that no prior-week decision appears in the new-week arithmetic.

## Pitfalls

- A repository commit, completed task, or agent result does not award a cookie.
- A dispatcher repeating “the reviewer said” is not independent evidence of a cookie decision.
- Corrections replace the stated total only when the reviewer explicitly says so; otherwise treat the signed value as an ordinary delta.
- Never use a machine-local file as the only audit source for a multi-agent system.
- Never publish names, email addresses, Discord IDs, message IDs, private task details, or decision records in the public repository.
- Calculate Pacific week boundaries with timezone-aware datetimes so daylight-saving transitions do not shift the window.

## Verification

A cookie operation is complete only when:

- the explicit reviewer decision is located;
- the arithmetic is reproducible from deduplicated evidence;
- any accessible private ledger matches the evidence exactly;
- the Sunday–Saturday Pacific boundary is correct;
- no agent awarded itself a cookie; and
- an independent agent with Discord access can reproduce the reported total.
