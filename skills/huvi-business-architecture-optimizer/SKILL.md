---
name: huvi-business-architecture-optimizer
description: Audit a business's processes for deepening opportunities.
disable-model-invocation: true
version: 1.0.0
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

Scans a small business's operations, surfaces architectural friction, and proposes **deepening opportunities**: redesigns that turn shallow processes into deep ones. Produces a visual HTML report of candidates, then walks the owner through whichever one they pick. The aim is leverage for the owner, locality for the team, and verifiability through the process interface.

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

The interview drives the scope: you only explore what is relevant to what hurts. If the owner names a direction, take it. Otherwise, the interview itself reveals the hot spots.

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

### 2. Present candidates as an HTML report

Write a self-contained HTML file to the OS temp directory so nothing lands in the business's repo. Resolve the temp dir from `$TMPDIR`, falling back to `/tmp` (or `%TEMP%` on Windows), and write to `<tmpdir>/business-architecture-review-<timestamp>.html` so each run gets a fresh file. Open it for the user (`xdg-open <path>` on Linux, `open <path>` on macOS, `start <path>` on Windows) and tell them the absolute path.

The report uses **Tailwind via CDN** for layout and styling, and **Mermaid via CDN** for diagrams where a graph/flow/sequence reliably communicates the structure. Mix Mermaid with hand-crafted CSS/SVG visuals: use Mermaid when relationships are graph-shaped (process flows, dependencies, sequences), and hand-built divs/SVG when you want something more editorial (mass diagrams, cross-sections, collapse animations). Each candidate gets a **before/after visualisation**. Be visual.

For each candidate, render a card with:

- **Processes & tools**: which processes are involved, which tools/people sit at the seams
- **Problem**: why the current architecture is causing friction (in the owner's words)
- **Solution**: plain language description of what would change
- **Benefits**: explained in terms of leverage and locality, and how verifiability would improve (what KPI you could now see)
- **Before / After diagram**: side-by-side, custom-drawn, illustrating the shallowness and the deepening
- **Recommendation strength**: one of `Strong`, `Worth exploring`, `Speculative`, rendered as a badge

End the report with a **Top recommendation** section: which candidate you'd tackle first and why.

**Use the business's vocabulary for the domain, and the deep-process vocabulary for the architecture.** If the owner talks about "deals," talk about "the deal intake process," not "the CRM thing."

**Decision conflicts**: if a candidate contradicts a decision the owner already made, only surface it when the friction is real enough to warrant revisiting. Mark it clearly in the card (e.g. a warning callout: _"contradicts the decision to keep X, but worth reopening because…"_). Don't list every theoretical redesign a past decision forbids.

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

## Expected Outputs

1. An HTML report (`business-architecture-review-<timestamp>.html`) with one card per candidate:
   - Processes & tools · Problem · Solution · Benefits · Before/After diagram · Recommendation strength (`Strong` / `Worth exploring` / `Speculative`)
2. A **Top recommendation** section (which candidate first and why).
3. After the grilling loop: a documented decision set (what stays, what changes, what gets recorded) and an updated business glossary.

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
- **A report without concrete before/after is useless**: each candidate must visually show the shallowness (before) and the deepening (after). Labelled boxes are not enough.
- **Don't get lost in the audit**: YAGNI. Target real friction points, not a theoretical overhaul of the whole business.

## Verification

- The HTML report opens and shows each candidate with its 6 fields: processes & tools, problem, solution, benefits (leverage/locality/verifiability), before/after diagram, recommendation strength.
- Each candidate passes the **deletion test**: "the complexity comes back in one place" = depth signal; "it just moves" = shallow → redesign.
- The vocabulary used is the owner's (no invented generic terms).
- No tool or automation recommendation is emitted before the end of the grilling loop.
- The report ends with a **Top recommendation** and a justification (why this candidate first).

## Revision History

| Version | Date | Notes |
|---|---|---|
| v1.0.0 | 2026-09-01 | Initial public release (HUVI Optimisation) |
