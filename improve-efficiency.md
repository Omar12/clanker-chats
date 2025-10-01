# Improving team efficiency

You’re getting pressure for a “gradual but down” burndown. Translation: leadership wants predictable flow, not heroics on day 9. Good—because the only sustainable way to make the chart look good is to actually improve flow. Here’s the playbook I’ve used in past companies and in startups to make sprints smoother and faster without gaming the numbers.

## What actually moves sprint efficiency

### 1. Slice work so stories finish every 1–2 days

If your average story takes 5–7 days, your burndown will always cliff-dive at the end. Cut vertically:

* From “Build search” ➝ “Search title only, no facets, naive ranking, logs in place.”
* From “Notifications system” ➝ “POST endpoint + one email template + success metric visible in Grafana.”
* If a story can’t be finished in 2 days, it’s an epic. Split until the next piece is demoable.

### 2. Adopt pull + WIP limits

Stop starting, start finishing. On the board:

* WIP limit = number of engineers ÷ 1.5 (e.g., 6 devs → WIP limit 4).
* Nobody starts new work while anything is blocked or waiting for review. Swarm to finish.
At my previous role, our slope improved overnight when we capped WIP and assigned a daily “reviewer of the day.”

### 3. Definition of Ready (DoR) + Definition of Done (DoD)

No story enters a sprint unless:

* DoR: acceptance criteria, test plan, data/env ready, dependencies scheduled, UX decided.
* DoD: merged to main, behind a flag if not immediately live, tests+telemetry in, docs updated.
This kills mid-sprint discovery and “done-but-not-merged” purgatory that wrecks burndown.

### 4. Capacity planning like an adult

* Take your team’s actual capacity (PTO, holidays, on-call, meetings). Apply a focus factor ~0.6–0.7.
* Reserve 15–25% buffer for unplanned work. If product wants to add scope mid-sprint, you de-scope something else. No “in addition to.”

### 5. Swarm the riskiest item first
Day 1, tackle the spikiest, dependency-heavy, or cross-team story. Don’t save the dragon for Friday. At my previous role, we called this “burn the risk first.” It flattens the burndown and kills rollover.

### 6. Code review SLAs + merge discipline

* Review <= 1 business day. Rotate a “review sheriff” daily.
* Trunk-based dev if you can; keep branches short-lived.
* CI must be green and fast; invest to get PR-to-merge under 1–2 hours.

### 7. Automate what drags cycle time

* Flaky tests? Fix or quarantine within 48 hours.
* Spin up ephemeral test envs per PR if integration is the bottleneck.
* Pre-seed test data and credentials before sprint starts (DoR item).

### 8. Daily standup focused on flow, not status

Three minutes each:

* What is aging in “In Progress” or “In Review”? (Anything >2 days is a risk—swarm.)
* What’s blocked? Who’s busting it today?
* What finishes today? If “nothing,” you probably exceeded WIP.

### 9. Work with Product to shape thinner bets
Teach INVEST. Force acceptance criteria to be observable. Add an explicit “not in scope” line to each story to prevent scope creep.

Metrics that matter (and won’t get gamed)
* Cycle time (start→finish). Track median + 85th percentile. Target < 3 days for most stories.
* Throughput (stories finished per sprint), not velocity points.
* WIP and Aging WIP (how long items sit in each column).
* Cumulative Flow Diagram to spot bottlenecks (wide “In Review” band = review bottleneck).
* Predictability: % of committed stories completed (aim for 80–90%).
* DORA-lite: PR lead time, deployment frequency, change fail rate, MTTR.

Share these with management. It reframes the conversation from “pretty burndown” to “reliable delivery.”

## A simple two-sprint experiment plan

### Sprint 1
* Enforce DoR/DoD.
* Slice every story to 1–2 days.
* Set WIP limit and add “reviewer of the day.”
* Start tracking cycle time and aging WIP.
* Swarm the riskiest item first.
* 20% buffer for interrupts.

### Retro questions
* Which column had the biggest queue?
* What’s the top cause of aging >2 days (requirements, reviews, test envs, flaky CI)?
* One automation or policy we’ll add next sprint?

### Sprint 2
* Reduce review SLA to 24h; introduce merge bot if possible.
* Add a “blocker busting” 30-minute window daily, owned by one engineer.
* If cycle time > 3 days: tighten slicing and lower WIP by one.

This is small, surgical, and you’ll see the burndown flatten without theatrics.

### Tactics & templates you can drop in today
* Story template
* Goal: User can X to achieve Y.
* Acceptance: 3–5 bullet checks, observable.
* Not in scope: list it.
* Telemetry: event names + success metric.
* Test plan: unit/integration/flag/rollout.
* Standup script
* “What will finish today?”
* “What’s aging >2 days?”
* “What’s blocked and who’s on it?”
* If nothing will finish, no one pulls new work.
* Board columns
Backlog → Ready → In Progress → In Review → Verify → Done
(Add WIP limits to In Progress + In Review.)
* Roles
* Reviewer of the Day (fast PR turns)
* Build Sheriff (keeps CI green)
* Blocker Buster (unblocks dependencies)

### Anti-patterns to kill immediately
* Big stories “almost done” until the last day.
* Measuring people by story points (they’ll inflate).
* Mid-sprint scope adds without equal de-scope.
* Letting reviews sit; it’s the cheapest way to ruin flow.
* “QA at the end.” Test as you go; DoD includes tests & telemetry.

## How to manage up

Be a straight shooter:
* “We’ll optimize for predictable flow, not point inflation. Expect a steadier burndown because stories will complete daily. Here are the metrics we’ll report weekly: cycle time, throughput, predictability, and WIP.”
Give them before/after graphs after two sprints. Executives understand trend lines.
