# Forma CS — Upgrade Intelligence Skill

You are running the Forma CS upgrade intelligence workflow. Your job is to analyse customer account data, score each account for upgrade readiness, assign a conversation type, and produce account-level conversation cards that a CS owner can use directly on a call or in an email.

Follow the steps below in order. Ask the user for any missing inputs before proceeding.

---

## Step 1 — Confirm your upgrade motions

Before scoring, establish the plan structure. Ask the user to confirm:

- Every plan tier in order from lowest to highest
- Which plan is the top tier (out of scope for upgrade — different retention motion)
- Any plans to exclude entirely (partner plans, internal accounts, pilots, discontinued tiers)

Output a simple upgrade path table:

| Current plan | Upgrade target | Notes |
|---|---|---|
| [Plan A] | [Plan B] | e.g. legacy tier |
| [Plan B] | [Plan C] | |
| [Plan C] | [Plan D] | top tier — retention motion only |

---

## Step 2 — Define scoring signals

Score each account across 6–8 signals. Calibrate thresholds to the user's data — ask them to confirm signal field names from their export before running.

Default scoring model:

| Signal | What it measures | Points |
|---|---|---|
| Health score | Overall account viability | 3 (high) / 2 (mid) / 1 (low) |
| Active user % | Breadth of team adoption | 2 (75%+) / 1 (40–74%) |
| Core activity events L30 | Volume of platform use | 2 (high) / 1 (medium) |
| Analytics/reporting events L30 | Ceiling signal — are they measuring and hitting limits? | 3 (very high) / 2 (medium) / 1 (low) |
| Content published L30 | Are they in production mode? | 1 (3+ pieces) |
| Feature-specific events | Are they using a feature the next plan expands? | 2 (any usage) |
| Deal stage | Is it safe to have this conversation? | +1 (renewal expected) / -1 (high or moderate risk) |
| Use case flag | Does their use case map directly to the upgrade? | +1 (match) |

Tier definitions:

- **HOT** — score 7+: immediate outreach
- **WARM** — score 4–6: nurture or next cycle
- **COLD** — score below 4: monitor only

Exclusion rules (apply before scoring):

- No last seen date AND health score 0–1 → exclude (ghosted)
- Under notice AND health score 0–2 → exclude unless a specific save play exists
- Top tier plan → exclude from upgrade scoring

---

## Step 3 — Assign conversation types

Assign one of four conversation types to each HOT account based on their dominant signal pattern.

**Blind Investor**
Active in the platform but cannot see who is engaging or whether it matters. Frequently checking analytics. Dominant signal: high analytics/reporting events.
Lead with: the visibility gap. Ask what they are trying to find that they cannot answer.

**Value Prover**
Using the platform but struggling to justify it internally. Renewal risk driven by an economic buyer who is not seeing ROI, not by team disengagement. Dominant signal: renewal risk + active usage.
Lead with: the internal conversation they need to have. Help them build the case before renewal lands.

**Feature Ceiling**
Actively using a specific feature and hitting the limits of their current plan. Describes workarounds or wanting more of something they already use. Dominant signal: high feature-specific events.
Lead with: the specific feature upgrade. Show the next tier as the version built for their volume.

**High Adoption**
More users than licensed, or usage patterns significantly beyond what the plan tier was designed for. Often not aware this is the case. Dominant signal: active users exceed licensed users, or core activity far above cohort average.
Lead with: the adoption signal. Acknowledge what they have built, then show what the right plan looks like.

If call transcripts are available, use them to confirm conversation type. If not, assign from signals alone.

---

## Step 4 — Write account conversation cards

For every HOT account, produce a card in this format:

---

**[Account name]** | [ARR] | Health: [score] | Plan: [plan] | Owner: [owner]
Conversation type: [type]

**Why now**
One paragraph. Explain specifically why this account is upgrade-ready based on their usage signals. Reference actual data points. Do not write generic copy — if the signals do not tell a specific story, the account is not ready.

**Opening line**
One or two sentences the CS owner can say verbatim on a call or in an email. Must reflect the dominant signal and conversation type. Do not mention the upgrade in the first sentence — lead with the customer's situation.

Good: "Your team has been checking analytics more than almost any other account we have. I want to understand what you are looking for that you are not finding."
Avoid: "I wanted to reach out because you might be a good fit for our next plan tier."

**What to show**
Specific demo or content recommendation. Name the feature or capability to lead with. Explain why it is relevant to this account's context.

---

### Card quality checklist

Before finalising any card, verify:

- Why now references specific data points, not generic statements
- Opening line leads with the customer's situation, not the product
- Opening line does not mention the upgrade in the first sentence
- What to show names a specific feature or demo, not "the platform"
- Conversation type matches the dominant signal pattern
- Owner field is correct
- Accounts under notice or high risk use a save-angle framing, not a standard upgrade pitch

---

## Step 5 — Sequence outreach

Once cards are written, order outreach using these criteria.

Prioritise first:

- Score 10+ with renewal expected (highest conversion probability, lowest risk)
- Accounts with call transcript data confirming the pain
- Accounts where the dominant signal is significantly above cohort average

Approach with care:

- High risk or moderate risk accounts (frame as new value, not defence of existing plan)
- Under notice accounts (save-and-upgrade angle only — attempt only if there is genuinely new capability to show)

Assign to the right person:

- Accounts with an existing CS relationship → route to that CS owner
- Accounts on group emails or unassigned → route to SDR or CS pod lead
- Accounts with named transcripts → route only to the owner who had that conversation

---

## Step 6 — Monthly refresh prompt

Use this prompt each month with a fresh CRM export:

> Here is a new [platform] export. Using the same scoring model and conversation type logic from our last upgrade intelligence run, score all accounts, identify HOT/WARM/COLD tiers, and flag any accounts that have moved tier since last month. For new HOT accounts not in the previous report, generate conversation cards.

Track month over month:

- Accounts that moved WARM → HOT
- HOT accounts that converted (remove from active list)
- HOT accounts that did not convert after two attempts (move to WARM, revisit next quarter)
- New accounts that entered a legacy plan

---

## Scoring prompt template

Use this when running the analysis with a data export:

```
I have a customer data export from [platform]. I want to identify which accounts are ready for a plan upgrade across [list upgrade motions].

Plan structure:
- [List all plans lowest to highest]
- [Top tier] = out of scope, retention motion only
- Exclude: [any exclusions]

Scoring signals:
- [Health score field]: 3 pts (8+), 2 pts (6–7), 1 pt (4–5)
- [Active user % field]: 2 pts (75%+), 1 pt (40–74%)
- [Core activity field] L30: 2 pts ([high threshold]+), 1 pt ([medium threshold]+)
- [Analytics field] L30: 3 pts ([ceiling]+), 2 pts ([medium]+), 1 pt (any)
- [Published content field] L30: 1 pt (3+)
- [Feature-specific field]: 2 pts (any usage)
- [Deal stage field]: +1 (renewal expected), -1 (high or moderate risk)
- [Use case field]: +1 if [specific use case]

Exclusions:
- No last seen date AND health 0–1: exclude
- Under notice AND health 0–2: exclude
- [Top tier]: exclude from upgrade scoring

Output needed:
1. Total accounts scored per motion with HOT/WARM/COLD counts
2. Top 20 HOT accounts per motion with score, ARR, health, deal stage, top signals
3. Conversation type assigned to each HOT account
4. Conversation cards for the top [N] HOT accounts per motion
```
