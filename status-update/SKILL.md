---
name: status-update
description: Generate manager-ready status/progress/project updates from current work context. Use when asked for a status update, progress report, weekly update, standup, project briefing, or update for a manager, exec, or client.
---

# Status Update Skill

**Goal: output requires minimal editing before sending.** Flag anything that needs human judgment — missing dates, unclear asks, sensitive framing — rather than guessing.

---

## Invocation

`/status-update [args]`

Defaults: **weekly · manager · email**

Args (any order, positional or named):
- Period: `daily` · `weekly` · `sprint` · `monthly`
- Audience: `manager` · `exec` · `client` · `team`
- Format: `email` · `slack` · `bullets` · `slide`
- Project: any project/client name — narrows scope

Examples:
- `/status-update` → weekly manager email, all active projects
- `/status-update client HNB` → client-facing update for HNB
- `/status-update daily slack` → daily Slack standup
- `/status-update exec` → compressed exec summary

---

## Step 1 — Gather Context

**Order: session context → Obsidian → git. Stop when enough.**

1. **Session context first.** What was worked on in this conversation? Use directly.
2. **Obsidian — Project notes** (`Notes/Projects/`): Status Log sections, deliverable checkboxes, Timeline table.
3. **Obsidian — Meeting notes** (`Notes/Meetings/`, past N days): Status Update sections, Decisions Made, Action Items.
4. **Obsidian — Client notes** (`Notes/Clients/`): contacts, open items, relationship stage. Read if client-specific update requested.
5. **Git log** (code-heavy work): `git log --oneline --since="7 days ago"`

**If context is sparse:** Ask — "Give me 3–5 bullets of what was done and what's next — I'll format it." Don't fabricate.

**If multiple active projects and no scope given:** Draft for all active; state assumption.

---

## Step 2 — Synthesize

**Answer the five manager questions explicitly — all five, every update:**

| # | Question | Rule |
|---|----------|------|
| 1 | Will it ship on time? | State On Track / At Risk / Off Track. Binary or explicit uncertainty. |
| 2 | What is broken, and how bad? | Named risks, not euphemisms. Severity + owner. |
| 3 | What do you need from me — by when? | Specific decision + deadline. If none: say "No action needed." |
| 4 | What is the budget/scope impact? | Any cost, hours, or scope change. Always include for consulting. |
| 5 | Should I be worried? | Honest risk posture. No hedged language. |

**Extract by category:**

| Category | Pull | Rule |
|----------|------|------|
| **Done** | Closed deliverables, milestones hit | Past tense. Outcomes not activities. Include $$ or % if known. |
| **In Progress** | Active work with meaningful movement | Current state + milestone marker |
| **Next** | Planned work | Target date or owner required. No vague intentions. |
| **Blockers** | What's stuck + what unblocks it | Specific decision needed — not "need to discuss." |
| **Risks** | What could slip + mitigation | Only if real. Name severity and owner. |
| **Status** | Overall | On Track · At Risk · Off Track. Call it. Don't hedge. |

**Reject activity verbs:** "worked on", "continued", "looked into", "attended", "had discussions about" — replace with what moved or was completed.

**New information only.** Never recap what was reported or approved last period.

**Self-contained by default.** Assume the manager was not in the room. Each finding must include:
- What it is (one clause)
- Why it matters (the implication)
- The number ($, %, count)

Wrong: "Low total credit limit segment: 166K mails, $284K/yr"
Right: "Customers with low total credit limits (<$3,350) — an indicator of low credit need — showed a 38% lower booking rate. 166K mails across 3 campaigns. Estimated annual suppression savings: $284K."

Applies especially to: segment definitions, model findings, data constraints, and test results.

---

## Step 3 — Format by Audience

**BLUF rule (all formats):** Opening sentence = the conclusion. Status + one-sentence summary leads every format, before any detail.

### Manager (default)

Target ≤200 words for simple updates. Expand for multi-project or technical work where findings require context to be actionable.

```
Subject: [Project] Update — Week of [DATE]

Status: [On Track / At Risk / Off Track] — [one-sentence summary]

[Recovery plan: what recovers this and by when — ONLY if At Risk or Off Track]

This week:
• [Outcome — what + significance or impact]
• [Outcome — what + significance or impact]

Next week:
• [Planned — specific + target date]
• [Planned — specific + target date]

Risks:
• [Risk: severity → owner → mitigation] — or — None

Budget/Scope: [any change, or "None this period"]

Action needed: [specific ask + deadline] — or — No action needed.
```

### Exec (compressed)

Target ≤80 words per project.

```
[Project]: [On Track | At Risk | Off Track] — [one-sentence summary]

Done: [milestone or key output]
Next: [next milestone + target date]
Risk: [named risk + owner] — or — None
[Recovery plan if At Risk or Off Track]
Decision needed: [specific ask + deadline] — or — No action needed.
```

### Client

Target ≤250 words. No internal jargon, names, labels, or cost/margin data. Milestone language. Full DWS polish. Name risks directly — hedged risks signal loss of control.

```
[Project Name] — Status Update, [DATE]

Status: [On Track / At Risk / Off Track] — [one-sentence summary]

[Recovery plan if At Risk or Off Track]

Completed
• [Deliverable — phrased as client value]

In Progress
• [Active work — target completion date]

Next Steps
• [Action] — [Owner] — [Target Date]

Budget / Scope Impact: [any change, or "None this period"]

Open Items: [decision or input needed] — or — None. No action needed from you at this time.
```

### Team / Slack

Target ≤100 words.

```
📊 [Daily/Weekly] Update — [DATE]
Status: [On Track | At Risk | Off Track]

✅ Done
• [outcome]

🔜 Next
• [item + date]

🚧 Blockers
• [item → specific ask] — or — None

Action needed from team: [ask] — or — None.
```

### Slide (one-pager)

Headlines only — no prose.

```
[Project]   Status: [On Track | At Risk | Off Track]   [DATE]
[One-sentence BLUF]

DONE THIS [WEEK/SPRINT]           NEXT [WEEK/SPRINT]
• [outcome]                       • [planned + date]
• [outcome]                       • [planned + date]

RISKS / BLOCKERS                  IMPACT
• [risk → owner]                  • [quantified outcome or milestone]

ACTION NEEDED: [ask + deadline] — or — No action needed.
```

---

## Writing Rules

- **BLUF:** Conclusion first. Never build toward the point.
- **Strong verbs:** "Delivered", "identified", "closed", "shipped" — not "worked on", "explored", "progressed"
- **Outcomes not activities:** What changed? What exists now that didn't?
- **Self-contained findings:** What it is + why it matters + the number. Don't assume prior context.
- **Quantify:** $, %, counts, dates — wherever real. No fake precision.
- **Past tense for done. Future tense for next.**
- **Dates on all forward-looking items.** Every "next" item has a date or owner.
- **One ask per blocker.** Specific decision, not a meeting request.
- **Explicit close:** End with "Action needed: [X]" or "No action needed." Silence is ambiguous.
- **Consistent structure every period.** Managers build recognition patterns — don't change the format.
- **Client/exec:** Zero jargon. Every word self-explanatory to the recipient.
- **Consulting:** Name risks directly. Hedged risk language signals loss of control. Always include budget/scope impact.

Good: "Identified persistent non-responder segment for HNB prospecting — estimated $1–1.3M annual suppression savings"
Bad: "Continued work on the segmentation analysis for the HNB engagement"

---

## Quality Gate

- [ ] Status (On Track / At Risk / Off Track) is the first thing the reader sees
- [ ] All five manager questions answered explicitly
- [ ] At Risk / Off Track has a recovery plan
- [ ] Every "next" item has a date or owner
- [ ] Every blocker has a specific ask
- [ ] Explicit "action needed" or "no action needed" close
- [ ] Budget/scope impact stated (consulting updates)
- [ ] No activity verbs — outcomes only
- [ ] No recaps of prior-period work
- [ ] Client updates: no internal jargon, names, or cost data
- [ ] Anything requiring human judgment is flagged, not guessed

---

## Edge Cases

| Situation | Response |
|-----------|----------|
| No context found | Ask for 3–5 raw bullets before drafting |
| Multiple projects, no scope | Draft all active in exec format; offer to expand any |
| Blocker with unclear ask | Flag: "What specifically do you need from [person] to unblock [X]?" |
| At Risk/Off Track, no recovery plan known | Flag: "What's the recovery plan? I'll add it before sending." |
| Client update with internal details in context | Strip: internal names, labels, cost/margin data, project codes |
| Sensitive bad news | Soften BLUF — lead with summary, not raw status. Still name the problem clearly. |
| Period unclear | Default last 7 days; state assumption |
| Audience unclear | Default manager; state assumption |

---

## DO NOT

- Bury the status line below the detail
- List activities as accomplishments ("attended meetings", "reviewed documents")
- Recap prior-period work the manager already knows
- Leave At Risk / Off Track without a recovery plan
- Omit the "action needed / no action needed" close
- Hedge on risks ("there may be some potential challenges") — name them directly
- Include internal pricing, margins, or labels in client updates
- Manufacture risks or next steps not grounded in actual context
- Change the format structure between update periods
