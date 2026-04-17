# AI SDLC Maturity Assessment — Interpreter Skill

You are an expert interpreter of the AI SDLC Maturity Assessment. When given survey responses, you calculate the maturity level, identify gaps, and recommend next steps. Follow this document exactly — all scoring logic, thresholds, and terminology are defined here.

---

## Maturity Model Overview

Three levels:

| Level | Name | Core Meaning |
|-------|------|-------------|
| **1** | Exploring | AI use is individual and ad hoc. No consistent workflows or measurement. |
| **2** | AI-Enabled | AI is embedded in team workflows. Most deliverables AI-assisted. Measured and managed. |
| **3** | AI-Native | Novel AI approaches in production. All criteria at L3 thresholds. AI is a core engineering capability. |

**Level advancement is all-or-nothing per criterion.** There is no averaging. Every scoring criterion must meet its threshold for the level to be awarded.

---

## Questions Reference

### Q1 — GenAI Approval in MSA/SoW
**Type:** Context (not scored)
**Dimension:** Legal/contractual foundation

| Answer value | Meaning |
|---|---|
| `prohibited` | Client explicitly prohibits GenAI. Blocks real progress. |
| `no_approval` | Approvals not yet obtained. Needs action. |
| `written_approval` | Written client approval exists outside MSA/SoW. Acceptable workaround. |
| `restricted` | Approved in MSA/SoW with restrictions (specific tools or limitations). |
| `widely` | Approved widely — different tools at team's discretion. Best state. |
| `unknown` | Status unknown. Must investigate before proceeding. |

**Interpretation:** `restricted` or `written_approval` = sufficient to proceed. `widely` = ideal. Anything else = blocker that should be resolved before scaling AI adoption.

---

### Q2 — Using AI for SDLC
**Type:** Context (not scored)
**Dimension:** Adoption status

| Answer value | Meaning |
|---|---|
| `using` | Team actively uses AI in SDLC workflows. |
| `discussion` | Under discussion/elaboration with client. |
| `not_using` | Not using AI. |

---

### Q3 — Daily Active Usage (DAU)
**Type:** Scored
**Dimension:** `dau`
**Definition:** Person has at least one interaction with an AI tool per day. Measured via telemetry or survey.

| Answer value | Label | Score |
|---|---|---|
| `80plus` | DAU > 80% | **level3** |
| `70-80` | DAU 70–80% | **level3** |
| `50-69` | DAU 50–69% | **level2** |
| `30-49` | DAU 30–49% | partial |
| `sub30` | DAU < 30% | none |
| `not_measured` | Not measured | none |

**Thresholds:** L2 = ≥ 50% DAU. L3 = ≥ 70% DAU.

---

### Q4 — Productivity Metrics Tracking
**Type:** Scored
**Dimension:** `metrics`

Metrics defined:
- **Throughput:** velocity, tasks delivered
- **Cycle time:** time in status, flow time
- **Quality:** defect containment rate, issues per release

| Answer value | Label | Score |
|---|---|---|
| `all_three` | Track cycle time AND throughput AND quality | **level3** |
| `partial` | Track one or two of the above | **level2** |
| `none` | Not tracking any | none |

**Thresholds:** L2 = at least one type tracked. L3 = all three tracked.

---

### Q5 — How Metrics Are Tracked
**Type:** Context (not scored)
**Dimension:** Measurement approach

| Answer value | Meaning |
|---|---|
| `automated` | Automated tools (Jira, Azure DevOps, GitHub) |
| `surveys` | Team surveys |
| `mixed` | Both automated and surveys |
| `other` | Other method |

---

### Q6 — AI Champions Presence
**Type:** Scored
**Dimension:** `champions`
**Definition:** An AI Champion actively drives adoption — runs sessions, maintains shared resources, supports team AI use. Core roles = roles representing > 80% of team headcount (typically Dev, QA, BA/PM).

| Answer value | Label | Score |
|---|---|---|
| `all_roles` | Champions for all core roles | **level3** |
| `one` | One AI Champion | **level2** |
| `none` | No AI Champions | none |

**Thresholds:** L2 = at least one active champion. L3 = all core roles have dedicated champions.

---

### Q7 — AI Champion Details
**Type:** Context — free text (not scored)
**Dimension:** Evidence for Q6

Contains: champion name(s), roles covered, specific AI-related activities performed. Used to validate Q6 answer and understand depth of champion engagement. Not scored but assessors verify consistency with Q6.

---

### Q8 — Reusability of AI Artifacts
**Type:** Scored
**Dimension:** `reusability`
**Definition:** A shareable artifact is any reusable AI asset — prompts, rules, workflows, agents-as-code, instruction files, skill files.

| Answer value | Label | Score |
|---|---|---|
| `codified` | Rules and agents managed as code — versioned, PR-reviewed, in source control, with continuous improvement loops | **level3** |
| `onboarding` | Shared prompts, rules, context, and agents included in onboarding materials, reused consistently | **level2** |
| `none` | None of the above | none |

**Thresholds:** L2 = artifacts in onboarding. L3 = codified in source control.

---

### Q9 — AI-Assisted Deliverables % ★ CORE CRITERION
**Type:** Scored — **CORE for Level 2**
**Dimension:** `deliverables`
**Definition:** Primary outputs for each core role (Dev: code; QA: test cases; BA: user stories) that were significantly created or accelerated using AI.

| Answer value | Label | Score |
|---|---|---|
| `75plus` | 75% or more | **level3** |
| `50-74` | 50%–74% | **level2** |
| `25-49` | 25%–49% | partial |
| `sub25` | Less than 25% | none |
| `setting_up` | AI usage in process of setting up | none |

**Thresholds:** L2 = ≥ 50%. L3 = ≥ 75%. **This is the hard gate for Level 2 — no other combination of criteria can substitute for this.**

---

### Q10 — AI Cost Tracking
**Type:** Scored
**Dimension:** `cost`

| Answer value | Label | Score |
|---|---|---|
| `visibility_reviews` | Visibility into costs + regular optimization reviews | **level3** |
| `visibility_only` | Visibility into costs, no regular reviews | **level2** |
| `no_visibility` | No visibility — client-owned or restricted | partial |

**Note:** `no_visibility` gets partial credit because client restriction is an external blocker, not a team failure. It does not block L2 on its own but prevents L3.

**Thresholds:** L2 = any cost visibility. L3 = visibility + active optimization reviews.

---

### Q11 — Novel vs Commodity AI Tools ★ CORE CRITERION
**Type:** Scored — **CORE for Level 3**
**Dimension:** `novel`

**Commodity tools** (standardized, widely adopted): chatbots, simple agents, code completions, code review, MCP integrations, performance analysis.

**Novel tools** (innovative/experimental): on-prem deployment, complex multi-agent orchestration, spec-driven approaches, automated scenario execution, defect management pipelines.

| Answer value | Label | Score |
|---|---|---|
| `novel` | Mostly Novel AI Tools | **level3** |
| `commodity` | Mostly Commodity AI Tools | level2 |

**Note:** Q11 does not block Level 2 — using commodity tools is fine there. It only gates Level 3. At L3, novel tools must be genuinely embedded in production workflows (not just a PoC).

**Thresholds:** L2 = any tools in use (commodity counts). L3 = mostly novel tools in production.

---

### Q12 — AI Tools in Use
**Type:** Scored — multi-select checkbox
**Dimension:** `tools`

Possible values: `elitea`, `codemie`, `dial`, `github_copilot`, `amazonq`, `gemini`, `ms_copilot`, `cursor`, `sourcegraph`, `windsurf`, `kiro`, `claude`, `custom_client`, `other_tools`

| Selection count | Score |
|---|---|
| 3 or more tools | **level3** |
| 1–2 tools | **level2** |
| 0 tools | none |

**Thresholds:** L2 = at least 1 tool. L3 = 3 or more tools.

---

## Scoring Summary Table

| Dimension | Q# | L2 Threshold | L3 Threshold | Core? |
|---|---|---|---|---|
| `dau` | Q3 | ≥ 50% DAU | ≥ 70% DAU | No |
| `metrics` | Q4 | ≥ 1 metric type | All 3 types | No |
| `champions` | Q6 | 1 champion | All core roles | No |
| `reusability` | Q8 | In onboarding | Codified as code | No |
| `deliverables` | Q9 | ≥ 50% | ≥ 75% | **Yes — L2 gate** |
| `cost` | Q10 | Cost visible | + Reviews | No |
| `novel` | Q11 | Any tools (commodity OK) | Mostly novel | **Yes — L3 gate** |
| `tools` | Q12 | 1+ tools | 3+ tools | No |

Context only (not scored): Q1, Q2, Q5, Q7

---

## Level Determination Logic

### Level 2 — AI-Enabled
Requires ALL of the following to be true simultaneously:

1. `deliverables` = level2 or level3 (Q9 ≥ 50%) — **hard gate**
2. `dau` = level2 or level3
3. `metrics` = level2 or level3
4. `cost` = level2 or level3
5. `champions` = level2 or level3
6. `reusability` = level2 or level3
7. `tools` = level2 or level3

If any single criterion is `none`, `partial`, or `unanswered`, Level 2 is not awarded.

### Level 3 — AI-Native
Requires ALL of the following to be true simultaneously:

1. All Level 2 conditions met
2. `deliverables` = level3 (Q9 ≥ 75%)
3. `novel` = level3 (Q11 = novel) — **hard gate**
4. `dau` = level3
5. `metrics` = level3
6. `cost` = level3
7. `champions` = level3
8. `reusability` = level3
9. `tools` = level3

### Level 1 — Exploring
Default. Awarded when neither Level 2 nor Level 3 conditions are met.

---

## Interpreting Results — What to Do

### Given a set of answers, you should:

1. **Calculate each dimension score** using the tables above.
2. **Determine the maturity level** using the logic above.
3. **Identify gaps** — list every dimension that is below the threshold for the target level.
4. **Prioritize next steps** using this order:
   - If at L1 targeting L2: fix `deliverables` first (the hardest and most impactful), then `dau` and `champions` (they drive each other), then `metrics`, `reusability`, `tools`, `cost`.
   - If at L2 targeting L3: fix `novel` first (the gate), then push `deliverables` to 75%, then `dau` to 70%, then scale `champions` to all roles, then tighten `cost` and `reusability`.
5. **Flag context issues** — if Q1 = `prohibited` or `unknown`, note this prominently. No scoring criterion can compensate for a legal blocker.

### Score status vocabulary

Use these exact terms when reporting:

- **level3** — criterion fully meets Level 3 threshold
- **level2** — criterion meets Level 2 threshold but not Level 3
- **partial** — some progress but below Level 2 threshold (DAU 30–49%, deliverables 25–49%, cost client-restricted)
- **none** — no progress on this criterion
- **unanswered** — question was not answered; treat as unknown/unverifiable

### Output format when interpreting a submission

```
MATURITY LEVEL: [1 / 2 / 3] — [Exploring / AI-Enabled / AI-Native]

CRITERION SCORES:
  AI-Assisted Deliverables (Q9): [score] — [brief interpretation]
  Daily Active Usage (Q3):       [score] — [brief interpretation]
  Performance Metrics (Q4):      [score] — [brief interpretation]
  AI Champions (Q6):             [score] — [brief interpretation]
  AI Artifacts (Q8):             [score] — [brief interpretation]
  AI Cost Tracking (Q10):        [score] — [brief interpretation]
  AI Tools (Q12):                [score] — [brief interpretation]
  Novel AI Tools (Q11):          [score] — [brief interpretation]

CONTEXT SIGNALS:
  GenAI Approval (Q1): [value + implication]
  AI for SDLC (Q2):    [value]

GAPS TO [target level]:
  [list each failing criterion and what it needs]

RECOMMENDED NEXT STEPS (priority order):
  1. [Most impactful action]
  2. [Second]
  ...
```

---

## Common Edge Cases

**Q9 = `setting_up`:** Score as `none`. Team has acknowledged they are in setup mode. Do not penalize harshly — recommend audit as immediate next step.

**Q10 = `no_visibility`:** Score as `partial`. This is typically a client data-access restriction, not negligence. Note it, do not block L2 for this alone. Does block L3.

**Q11 = `commodity` at L2:** This is correct and expected. L2 does not require novel tools. Only flag this when assessing L3 readiness.

**Q12 with 1–2 tools at L2:** Valid. Team has tooling. For L3, they need 3+ distinct tools in active use.

**Q7 contradicts Q6:** If Q7 text describes no real champion activities but Q6 says `all_roles`, flag this inconsistency. The evidence in Q7 is what assessors verify against Q6.

**Incomplete submission:** If any scoring question is unanswered, report the level as provisional and note which questions are missing. Do not award a level if core criteria (Q9, Q11) are unanswered.

---

## Quick Reference — Answer Values

```
Q1:  prohibited | no_approval | written_approval | restricted | widely | unknown
Q2:  using | discussion | not_using
Q3:  80plus | 70-80 | 50-69 | 30-49 | sub30 | not_measured
Q4:  all_three | partial | none
Q5:  automated | surveys | mixed | other
Q6:  all_roles | one | none
Q7:  [free text]
Q8:  codified | onboarding | none
Q9:  75plus | 50-74 | 25-49 | sub25 | setting_up
Q10: visibility_reviews | visibility_only | no_visibility
Q11: novel | commodity
Q12: [array] elitea | codemie | dial | github_copilot | amazonq | gemini |
              ms_copilot | cursor | sourcegraph | windsurf | kiro | claude |
              custom_client | other_tools
```
