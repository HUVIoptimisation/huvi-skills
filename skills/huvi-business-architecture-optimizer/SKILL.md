---
name: huvi-business-architecture-optimizer
description: Audit a business's processes for deepening opportunities.
disable-model-invocation: true
version: 1.1.0
author: HUVI Optimisation
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [huvi, architecture, processus, business, deepening, deletion-test, html-report]
    related_skills: []
---

# HUVI Business Architecture Optimizer

## What This Skill Does

Scans a small business's operations, surfaces architectural friction, and proposes **deepening opportunities**: redesigns that turn shallow processes into deep ones. Produces a structured visual HTML report — an overall verdict, a summary table, and **one detailed fiche per candidate process** — then walks the owner through whichever one they pick. The aim is leverage for the owner, locality for the team, and verifiability through the process interface.

## When to Use It

- The owner or operator of a small business (services, construction, trades) wants to find out why their operations feel heavy, where time and money leak, or how to prepare a process for automation.
- An agent is asked to audit, restructure, or "put on autopilot" a business's operations — BEFORE any tool or automation is chosen.
- A business wants a visual, prioritized list of process redesigns to work through.

## Design Vocabulary

This command is _informed_ by the business's domain model and built on a shared design vocabulary:

- **Process** — anything with an interface and an implementation. Scale-agnostic: a lead capture, a quotation, a handoff, a billing cycle. _Avoid_: "department", "task", "workflow" (too vague or too narrow).
- **Interface** — everything an actor must know to run the process correctly: the inputs required, the steps, the ordering constraints, the error modes, the tools involved.
- **Depth** — leverage at the interface. A process is **deep** when a large amount of behaviour sits behind a small interface (one normed input → structured output). It is **shallow** when the interface is nearly as complex as the implementation (many steps to know, many exceptions, pass-throughs).
- **Seam** — a place where you can change how the process behaves without editing the process itself: the handoff point between two processes, the tool boundary. _Avoid_: "boundary".
- **Adapter** — a concrete thing that satisfies a process at a seam: the CRM, the spreadsheet, the automation, the form.
- **Leverage** — what the owner gets from depth: more results per unit of effort. One deep process pays back across every employee, every client, every week.
- **Locality** — what the team gets from depth: knowledge, data, and fixes concentrate in one place (the single source of truth) instead of spreading across texts, spreadsheets and inboxes.

Use these terms exactly in every suggestion. Don't drift into "department", "tool", "task", or "operation".

**Ground rules:**
- **The golden rule: you never automate chaos.** Adding technology (CRM, AI, automation) to a bad process only creates errors faster. Deepening comes BEFORE automation — always.
- **The deletion test.** Imagine deleting the process. Does the complexity vanish, or does it reappear across N people, tools and workarounds? If it reappears, the process earns its keep. If it just moves (manual work, someone's head, another tool), it is shallow — redesign or remove it.
- **The interface is the verification surface.** If you want to verify "past" the interface (can't see the state of the process without asking someone), the process is probably the wrong shape.
- **One adapter means a hypothetical seam. Two adapters means a real one.** Don't introduce a tool/automation at a seam unless something actually varies across it.
- **The business's own language names the seams.** Use the owner's vocabulary (their leads, their deals, their projects) — never generic labels.

**Epistemic registers — always distinguish, in every fiche and every sentence that asserts:**
- **FACT** — what the business demonstrably does: observed, counted, documented.
- **INFERENCE** — the reasonable reading of something ambiguous or unverified, and why it is a reading, not a fact.
- **RECOMMENDATION / RISK** — what the owner should verify, redesign, or reject.

Never invent a process step, a volume, or a number. If the business has no trace of something, say so: an absence is not a process, it is a risk (the work happens in someone's head, in texts, in a spreadsheet no one updates).

## Modes

Two modes, decided at step 0 and announced in the report header:

| | **QUICK** | **FULL** |
|---|---|---|
| **When** | Small business, one clear pain point, owner wants a direction fast | Business with several flows, scattered tools, or the owner wants the complete picture |
| **Fiche depth** | Verdict + essentials, deletion test, top 3 frictions, redesign priorities | Every fiche section below, fully |
| **Candidates** | 2-4, focused on the named pain | Up to the scope revealed by the interview |

Rule: when in doubt → FULL. The owner can force a mode by saying so.

## Process

### 0. Interview the owner first (business analysis)

Before exploring anything, run a deep interview. Ask real questions, one topic at a time, and take notes — the answers define the scope of the whole audit. Cover:

- **The business**: industry, offer, size, team composition, typical clients, volume (leads/projects per week or month)
- **Current architecture**: every tool in play (CRM, spreadsheets, apps, messaging), where the data actually lives, who does what, what talks to what
- **The main flows**: the core chain (lead → quote → project → billing) — step by step, in their words; what is documented vs. what lives in their head
- **Pain points**: where time leaks, where mistakes repeat, where information gets lost, what keeps them busy in the evenings, which tasks they dread
- **Data & steering**: which numbers they track (if any), dashboards, time sheets, how they know a job was profitable
- **Past decisions**: what was tried and rejected (tools, processes, hires) and why — never re-suggest these
- **Goals**: why now, where they want the business to be in 6-12 months, what "freedom" looks like

The interview drives the scope: you only explore what is relevant to what hurts. If the owner names a direction, take it. Otherwise, the interview itself reveals the hot spots. Record the mode (quick/full) you will run.

### 1. Explore

**Scope before you scan: YAGNI.** Deepening a process pays off by making future changes to it easier, so put extra weight on the parts of the business that hurt most. Decide _where_ to look before you look:

- If the owner named a direction (a process, a pain point, a recurring headache), take it, and skip the inference below.
- Otherwise, ask what keeps coming up: where does the owner spend their evenings? Where do mistakes happen repeatedly? Where does information get lost? Where do clients complain? Let those pull your attention first. If the pain is scattered with no clear hot spot, widen the net.

Collect the business's vocabulary first (what is a "lead", a "deal", a "project", a "change order" in THEIR words) and note any decisions already made (things that were tried and rejected) so you don't re-suggest them.

Then walk the business's processes. Don't follow rigid heuristics; explore organically and note where you experience friction:

- Where does understanding one process require bouncing between many small tools and people?
- Where are processes **shallow**, with an interface nearly as complex as the implementation (every step is a special case)?
- Where has work been "extracted" into tools, but the real problems hide in how they're called (no **locality** — the data lives in 5 places)?
- Where do tightly-coupled processes leak across their seams (the handoff between sales and operations)?
- Which parts of the business are unverifiable, or hard to verify through their current interface (no KPI, no dashboard, no paper trail)?

Apply the **deletion test** to anything you suspect is shallow: would removing it concentrate complexity, or just move it? A "yes, concentrates" is the signal you want.

### 2. Present the report

Write a self-contained HTML file to the OS temp directory so nothing lands in the business's repo. Resolve the temp dir from `$TMPDIR`, falling back to `/tmp` (or `%TEMP%` on Windows), and write to `<tmpdir>/business-architecture-review-<timestamp>.html` so each run gets a fresh file. Open it for the user (`xdg-open <path>` on Linux, `open <path>` on macOS, `start <path>` on Windows) and tell them the absolute path.

The report uses **Tailwind via CDN** for layout and styling, and **Mermaid via CDN** for diagrams where a graph/flow/sequence reliably communicates the structure. Mix Mermaid with hand-crafted CSS/SVG visuals: use Mermaid when relationships are graph-shaped (process flows, dependencies, sequences), and hand-built divs/SVG when you want something more editorial (mass diagrams, cross-sections, collapse animations). Each fiche gets a **before/after visualisation**. Be visual.

**Report structure (follow it exactly):**

```
# Business Architecture Review — [Business name]
Owner: [role] · Mode: quick/full · Date: [date]
## 0. Overall verdict — decision first, 5 lines max
## 1. Summary table of process fiches
   | Process | Verdict | Depth | Owner cost | Priority |
## 2. Detail fiches — one per candidate process (Fiche Structure below)
## 3. Top recommendation — which process first and why
```

**Fiche Structure (one per candidate process):**

```
## Fiche — [Process name, in the owner's words]
### 1. Verdict and essentials — decision first, 5 lines max
   Verdict badge + the top points to settle, in plain language.
### 2. What actually happens (FACT / INFERENCE / RECOMMENDATION)
### 3. Depth — interface vs complexity
   Small table: normed input? logic encapsulated? structured output?
   exceptions handled? single source of truth? → shallow or deep.
### 4. Deletion test
   Deleted, where does the complexity go? Vanish, or scatter across
   people/tools/heads? Verdict: deep (protect) or shallow (redesign).
### 5. Frictions and risks
   Table: friction | concrete impact | level (LOW/MEDIUM/HIGH) | what to do.
### 6. Current costs
   Time per week, money, cognitive load (owner's evenings).
### 7. Value vs effort
   Table showing where value is delivered vs where effort is spent —
   the asymmetry is the opportunity.
### 8. Redesign — 3 priorities maximum, ranked
   MUST CHANGE / SHOULD CHANGE / NICE TO HAVE. For each: why it
   matters, the outcome to aim for, a fallback. Automation only ever
   appears here as the LAST step of a priority — after the process is deep.
### 9. Missing information before deciding
   What would change the verdict, and how to get it (count for 2 weeks,
   check the log, ask the team).
```

**Verdict badges** (one per fiche, decision first):

- 🟢 **DEEP** — the process concentrates complexity behind a small interface. Protect it, extend it, document it. No redesign needed.
- 🟡 **SHALLOW** — the interface is as complex as the implementation; the process moves work around instead of absorbing it. Redesign before automating.
- 🔴 **FRAGILE** — shallow AND acting up: silent failures, dependence on one person, unmanaged exceptions. Intervene soon.
- ⚫ **REMOVE** — negative ROI (maintenance and attention cost more than the value), or a duplicate of another process. Delete or merge.

Each fiche cites the owner's vocabulary and marks the **epistemic registers** (FACT / INFERENCE / RECOMMENDATION) throughout. Every risk is rated. The QUICK mode produces a leaner fiche (verdict + essentials, deletion test, top 3 frictions, priorities) but keeps the header, the verdict, and the registers.

**Vocabulary and decision conflicts:** use the business's vocabulary for the domain, and the deep-process vocabulary for the architecture. If the owner talks about "deals," talk about "the deal intake process," not "the CRM thing." If a candidate contradicts a decision the owner already made, only surface it when the friction is real enough to warrant revisiting. Mark it clearly in the fiche (e.g. a warning callout: _"contradicts the decision to keep X, but worth reopening because…"_). Don't list every theoretical redesign a past decision forbids.

Do NOT propose tools or automations yet. After the file is written, ask the owner: "Which of these would you like to explore?"

### 3. Grilling loop

Once the owner picks a candidate, walk the decision tree with them: constraints, dependencies, the shape of the deepened process, what sits behind the seam, what stays manual.

Side effects happen inline as decisions crystallize:

- **Naming a deepened process after a concept the owner uses?** Write it down in the business glossary (create the file lazily if it doesn't exist).
- **Sharpening a fuzzy term during the conversation?** Update the glossary right there.
- **Owner rejects the candidate with a load-bearing reason?** Offer to record it, framed as: _"Want me to note this down so future reviews don't re-suggest it?"_ Only offer when the reason would actually be needed by a future explorer to avoid re-suggesting the same thing; skip ephemeral reasons ("not worth it right now") and self-evident ones.
- **The owner wants to explore alternative shapes for the deepened process?** Sketch 2-3 radically different shapes, then compare on depth, locality, and seam placement. Design it twice.

**Only after the process is deep and documented: automation.** Apply the golden rule — the tool comes last. When the owner asks about automating, scope it as: normed input → structured output → one clear trigger. If the process isn't deep yet, say so.

## Inputs

- Business context (string): industry, size, team composition, current tools (optional but recommended)
- Pain points / direction (string): a named process or recurring headache to focus on (optional — otherwise discovered)
- Business vocabulary / glossary (string): the owner's terms for leads, deals, projects, change orders (optional)
- Past decisions (string): what was tried and rejected, so nothing is re-suggested (optional)
- Mode (string, optional): quick or full — otherwise decided at step 0

## Expected Outputs

1. An HTML report (`business-architecture-review-<timestamp>.html`) following the report structure above:
   - Overall verdict (decision first)
   - Summary table of process fiches (process | verdict | depth | owner cost | priority)
   - One **fiche per candidate process** with: verdict badge 🟢🟡🔴⚫ · essentials · what actually happens (FACT/INFERENCE/RECOMMENDATION) · depth table · deletion test · frictions rated · current costs · value vs effort · 3 redesign priorities ranked · missing information
   - Before/After visualisation per fiche
   - **Top recommendation** section (which process first and why)
2. After the grilling loop: a documented decision set (what stays, what changes, what gets recorded) and an updated business glossary.
3. Every assertion tagged FACT / INFERENCE / RECOMMENDATION — nothing invented, absences called out as risks.

## Example Prompt Pattern

```
My [type of business] is losing [asset — leads, time, money] between [tools/places]
and I spend my evenings [pain — doing devis, chasing hours, answering the same questions].
Audit my processes and tell me what to redesign.
```

## Dependencies

- None required (self-contained). A browser is needed to open the HTML report (Tailwind/Mermaid loaded via CDN).
- Optional: an HTML report renderer / local browser for the `xdg-open` / `open` / `start` step.

## Related Assets

*Link to agents and prompts using this skill.*

## Pitfalls

- **Never propose a tool or an automation before the process is deep** — the golden rule ("you never automate chaos") is non-negotiable. The grilling loop ends with automation, never the reverse.
- **Don't invent business vocabulary**: use the owner's terms (their leads, their deals, their sites). Generic labels = a report that speaks to no one.
- **Don't re-suggest a decision already made**: check the decision record before proposing. Only reopen a file if the friction is real and documented.
- **A report without concrete before/after is useless**: each fiche must visually show the shallowness (before) and the deepening (after). Labelled boxes are not enough.
- **Don't get lost in the audit**: YAGNI. Target real friction points, not a theoretical overhaul of the whole business.
- **Never invent a fact**: no step, volume, or number without a source. No trace of something = state the absence (FACT: no record exists) and flag the risk — don't guess the number.
- **A fiche without a verdict is a memo**: every candidate process gets a 🟢🟡🔴⚫ badge, decision first. If you can't decide, the "Missing information" section is where the blocker goes, not a wishy-washy verdict.
- **Don't recommend removing a process the owner depends on daily** without showing what absorbs the complexity (deletion test, section 4 of the fiche).

## Verification

- The HTML report opens and shows: overall verdict, summary table, one fiche per candidate with all its sections (verdict badge, registers, depth, deletion test, rated frictions, costs, value vs effort, 3 priorities, missing info), before/after visualisation, and a top recommendation.
- Each fiche passes the **deletion test**: "the complexity comes back in one place" = depth signal; "it just moves" = shallow → redesign.
- Every assertion in every fiche is tagged FACT / INFERENCE / RECOMMENDATION. Absences are stated as absences, never filled in.
- The vocabulary used is the owner's (no invented generic terms).
- No tool or automation recommendation is emitted before the end of the grilling loop.
- The report ends with a **Top recommendation** and a justification (why this process first).

## Revision History

| Version | Date | Notes |
|---|---|---|
| v1.0.0 | 2026-09-01 | Initial public release (HUVI Optimisation) |
| v1.1.0 | 2026-09-05 | Bonification of the output format: per-process fiches with verdict badges (🟢 DEEP / 🟡 SHALLOW / 🔴 FRAGILE / ⚫ REMOVE), epistemic registers (FACT/INFERENCE/RECOMMENDATION) throughout, formal fiche structure (depth table, deletion test section, rated frictions, costs, value vs effort, 3 ranked redesign priorities, missing information), QUICK/FULL modes, overall verdict + summary table in the report header. Scope unchanged: business processes before automation. |
