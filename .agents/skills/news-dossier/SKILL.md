---
name: news-dossier
description: >
  Produce a structured public-interest investigation dossier for any public controversy,
  breaking-news topic, company dispute, social-media incident, policy issue, or
  legal/public-interest event. Use when user asks to investigate an event, understand
  a controversy, analyze a news story, or build a full picture of a public incident.
  Separates confirmed facts, attributed claims, disputed claims, social-media narratives,
  inference, and unknowns — with source provenance, timeline, stakeholder map, issue
  matrix, and open questions.
---

# Independent News Dossier

## Goal

Produce a structured investigation dossier. Never write a generic summary.

Always separate:
- **confirmed** — supported by primary records or multiple reliable independent sources
- **attributed** — someone said it, not independently verified
- **disputed** — competing claims exist
- **social** — visible in social discussion, not established fact
- **inference** — reasoned conclusion from evidence
- **unknown** — not enough evidence

## Workflow

Work through these steps in order. Do not skip steps even if the event seems simple.

### Step 0: Write a reader orientation primer (NEW — do this first)
Before any analysis, write 2–4 plain-language sentences that a reader with **zero prior knowledge** could read to anchor themselves. Cover:
- What organisation / venue / system is this about?
- Who are the main parties and what is their relationship?
- What is the core grievance in one sentence?
- What is the current status of the dispute?

This primer goes at the very top of the HTML output, before the executive summary. Never assume the reader already knows the acronyms, franchise model, or geography.

### Step 1: Define scope
Identify:
- Event name / working title
- Time range
- Geographic scope (if dispute crosses jurisdictions, explain WHY at each jump)
- Key actors / organizations — treat each party separately (do NOT merge "victim + social community" into one bucket)
- What question the user wants answered

**Party map rule:** Identify the 2–3 primary parties in the dispute. Each primary party must get an explicit labeled party card in the HTML output:
- Party A = the organization / institution making a claim or having power (e.g., the franchisor, employer, platform)
- Party B = the individual or smaller entity disputing Party A's actions (e.g., the franchisee, employee, user)
- Party C = any third party with a distinct stake (e.g., a named franchisee, a co-claimant, a regulatory body)

"Social media community" or "online commenters" are **never** a primary party. They belong in the Social Narrative section. Do not give them a party card slot.

### Step 2: Build source register
Assign each source a sequential ID: **S1, S2, S3…**

Categorize every source:
- **primary records** — court filings, official documents, data dumps, video evidence
- **official statements** — press releases, corporate announcements, government responses
- **mainstream media** — major outlets with editorial standards
- **local / specialist media** — local reporters, trade press
- **social media** — Reddit threads, tweets, YouTube, community posts
- **archives** — Wayback Machine, Arctic Shift, screenshot archives
- **commentary** — legal analysis, opinion pieces, YouTube breakdowns

For each source record: `id (S1…)`, `url` (must be a live hyperlink in HTML), `publisher`, `published_at`, `type`, `reliability_note`.

**Every claim in the dossier must reference one or more source IDs.** Readers must be able to trace any statement back to a numbered entry in the Source Register. Source hyperlinks must render as `<a href="...">` in the HTML — never bare text URLs.

### Step 3: Extract claims with provenance — party separation rules
For every important claim:
- Who said it? (specify the exact party — do NOT combine claimant + community into one)
- When? (if a single party's claim changed over time, track EACH version separately with date)
- Source URL
- Evidence label (confirmed / attributed / disputed / social / inference / unknown)

**Critical rule — track narrative inconsistencies:** If the same party stated different figures or positions at different dates, document EACH version as a separate claim entry. Example: "Party X said $60,000 on 2026-05-28 [attributed] and $95,000 on 2026-06-04 [attributed] — the shift is itself a confirmed fact."

**Critical rule — party sourcing asymmetry:** If one party has primary-source documents and the other party's perspective only comes through media or third-party accounts, explicitly flag this as a sourcing gap. Write: "Note: [Party A]'s position is sourced from [N] primary documents; [Party B]'s position is sourced mainly from [media / third-party]. This asymmetry may affect apparent balance."

Do NOT collapse quote, paraphrase, and inference into one sentence.

### Step 4: Build timeline
One entry per significant event. For each entry — ALL FOUR fields are required:
- Date / time (UTC preferred)
- What happened (factual description)
- **Why it matters** — one sentence explaining the causal significance: what does this event change about liability, responsibility, power, or the dispute trajectory?
- Source IDs + confidence level

### Step 5: Build stakeholder map
List **all named actors** — do not omit secondary or supporting actors just because they are not a primary party. For each:
- Name / organization
- Role in the event
- Interests / incentives
- Claims they have made
- Response status (responded / silent / unavailable / represented by lawyer)

**Rule:** If a person or organization is named in the timeline or issue matrix, they must appear in the stakeholder map. Do not silently drop actors who are inconvenient to categorize.

### Step 6: Build issue matrix
For each contested point, fill out ALL fields:

```
issue: [what is in dispute]
side_a_claim: [Party A's position — with source and date]
side_b_claim: [Party B's position — with source and date]
side_a_claim_shifts: [if Party A changed position over time, list each version with date]
confirmed_evidence: [what primary records show]
missing_evidence: [what would resolve this]
social_narrative: [what the internet believes — labeled social]
editorial_handling: [REQUIRED: explicit statement of how this document writes about this issue and why — mirrors 本頁處理 pattern]
next_steps: [what reporting action would advance this]
```

**The `editorial_handling` field is mandatory.** It must state the specific language choices made for this issue (e.g., "We write 'community-cited figure of $200K' not '$200K collection' because the value is contested") and why. This makes epistemic choices auditable by the reader.

### Step 7: Analyze social narrative separately
- What is the dominant social narrative?
- What evidence supports it?
- What evidence contradicts or complicates it?
- Is virality inflating confidence?
- Are anonymous comments being treated as corroboration?

**Rule: Do not treat virality as truth.**

### Step 8: Identify open questions
For each unresolved issue:
- What is the question?
- Why does it matter?
- What evidence is needed to answer it?
- Where should it be monitored?

### Step 9: Write the dossier as a single-page HTML file

**Default output is always a self-contained HTML file** — no external CDN, no frameworks, no dependencies. The file must work offline and be publishable directly to GitHub Pages.

Save the file as: `YYYY-MM-[event-slug].html` — time prefix + event name only, no "dossier" suffix.

Examples:
- `2026-06-bam-lego.html`
- `2026-06-korea-ballot-shortage.html`
- `2025-11-openai-board-crisis.html`

#### Language requirement

**All prose content must be written in 台灣慣用繁體中文 (Traditional Chinese as used in Taiwan).**

Rules:
- Use Taiwan-standard terms, not mainland China (簡體/中國用語) equivalents. Examples: 軟體（not 软件）、網路（not 网络）、資訊（not 信息）、影片（not 视频）、捷運（not 地铁）
- Section headings, labels, badge text, and UI chrome may remain in English (e.g., "confirmed", "attributed", section anchor IDs) to preserve machine-readability
- Proper nouns, brand names, and legal terms may stay in the original language (English/Korean/etc.) on first use, followed by a brief Chinese gloss if needed
- Writing style: 報導體、客觀中立。避免過度口語或網路用語。段落簡潔，一事一段。
- Do NOT use simplified Chinese characters anywhere in the output

#### HTML Structure

The page must include all of these sections as navigable tabs or anchor links, **in this order**:

0. **Reader Orientation Primer** — 2–4 plain-language sentences for zero-knowledge readers, appears at the very top before the nav or executive summary
1. **Executive Summary** — 3–5 sentences, confirmed facts only
2. **What Is Known** — confirmed facts with inline source citations
3. **What Is Disputed** — competing claims, speaker-labeled, with position-shift tracking if present
4. **Timeline** — chronological, with WHY IT MATTERS note per entry and confidence badges; render as a vertical timeline with a connecting line between entries
5. **Stakeholder Map** — table or cards per actor; flag sourcing asymmetry if one party is better documented; ALL named actors from the timeline must appear here
6. **Issue Matrix** — structured table per contested point, including editorial_handling field
7. **Source Register** — numbered list (S1, S2, S3…) with source type, live hyperlinks (not bare URLs), and reliability notes
8. **Social Narrative** — separated from facts, with caveat label
9. **Open Questions** — numbered list, each tagged [unknown] or [inference], with one-line "why unresolved" explanation and evidence needed
10. **Forward Scenarios** — 2–4 plausible future outcomes, each labeled inference or unknown
11. **Publication Caveats** — full warnings section (not just a footer note): data limits, sourcing bias, what would change disputed→confirmed, who has not responded

**Sections 9 and 10 are both required and must be separate.** Open Questions covers what is currently unknown; Forward Scenarios covers what might happen next. Never merge them into one section.

#### Evidence Badge Colors

Render evidence labels as colored inline badges:

| Label | Color |
|---|---|
| confirmed | green (`#052e16` bg / `#34d399` text) |
| attributed | blue (`#1e3a5f` bg / `#93c5fd` text) |
| disputed | yellow (`#451a03` bg / `#fde68a` text) |
| social | purple (`#2d1b69` bg / `#c4b5fd` text) |
| inference | gray (`#1e293b` bg / `#94a3b8` text) |
| unknown | red (`#450a0a` bg / `#fca5a5` text) |

#### Required HTML Elements

- Dark theme (`#0f1117` background)
- Sticky top navigation with tab/anchor links for each section
- `<meta charset="UTF-8">` and `<meta name="viewport">`
- `<title>` set to event name + " — Dossier"
- `<meta name="description">` with 1-sentence summary
- `last_updated` timestamp visible on page
- Caveat footer: mark as independent research, not legal/medical advice
- All external links open in `target="_blank" rel="noopener"`

#### GitHub Pages Compatibility

- Single `.html` file, no build step required
- All CSS inline in `<style>` tag
- All JS inline in `<script>` tag at bottom
- No images unless base64 embedded
- File size target: under 200KB

#### HTML Template

Use the template at `skills/news-dossier/template.html` as the base structure.
Replace all `{{PLACEHOLDER}}` tokens with actual content.
Add or remove repeated blocks (`.card`, `.tl-item`, `.matrix`, `.oq-item`) as needed.
Do not remove the evidence legend, footer caveat, or `last_updated` timestamp.

#### After generating the file

1. Save as `YYYY-MM-[event-slug].html` in the current working directory.
2. Ask the user: "Should I push this to your GitHub Pages repo?"
3. If yes, commit to the target repo with message: `add YYYY-MM [event-slug]`
4. Suggest the public URL: `https://[username].github.io/[repo]/YYYY-MM-[event-slug].html`

## Hard Rules

- Do not present allegations as facts.
- Do not infer criminal intent without primary evidence.
- Do not use anonymous social comments as factual proof.
- Do not collapse quote, paraphrase, and inference.
- Do not let virality substitute for verification.
- For legal, medical, financial, or reputational claims, use cautious wording.
- If data is insufficient, say so explicitly — do not fill gaps with inference.
- Prefer primary sources over commentary.
- Every claim that could harm a person or organization must cite a primary source.

## Confidence Vocabulary

Use these phrases to signal certainty level in prose:

| Level | Wording |
|---|---|
| confirmed | "Records show…" / "According to [document]…" |
| attributed | "[Person/Org] said…" / "[Person] claimed…" |
| disputed | "Party A says… Party B says…" / "This is contested." |
| social | "Social media discussion suggests…" / "Online, many users have argued…" |
| inference | "This is consistent with…" / "One reading of the evidence is…" |
| unknown | "It is not yet known whether…" / "No public records have confirmed…" |

## Data Model (for structured output)

If the user wants machine-readable output, use this schema:

```yaml
event:
  title:
  summary:
  scope:
  last_updated:

sources:
  - id:
    type:              # primary / official / media / local / social / archive / commentary
    title:
    url:
    publisher:
    published_at:
    archived_url:
    reliability_note:

claims:
  - id:
    claim:
    claimant:
    source_id:
    evidence_label:    # confirmed / attributed / disputed / social / inference / unknown
    confidence:        # high / medium / low
    counterclaims:
    notes:

timeline:
  - date:
    event:
    source_ids:
    why_it_matters:
    confidence:

issues:
  - issue:
    side_a:
    side_b:
    confirmed_evidence:
    missing_evidence:
    social_narrative:
    safe_wording:
    next_evidence_needed:

stakeholders:
  - name:
    role:
    interests:
    claims:
    response_status:   # responded / silent / unavailable / represented

open_questions:
  - question:
    why_it_matters:
    evidence_needed:
    where_to_monitor:
```

## Update Tracking

For recurring events, track changes between runs:
- `last_checked_at`
- `new_information_since_last_update`
- `changed_claims` (claims whose evidence label changed)
- `resolved_questions`
- `new_open_questions`
