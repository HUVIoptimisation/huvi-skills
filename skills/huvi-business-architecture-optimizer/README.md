# huvi-business-architecture-optimizer

Audits a business's processes and proposes **deepening opportunities** — redesigns that turn
shallow processes into deep ones — presented as a structured visual HTML report (overall
verdict + one detailed fiche per candidate process), then grilled through with the owner.

## When to use

- You feel your operations are heavy and you don't know where time and money leak.
- You want to prepare a process for automation the RIGHT way (structure first, tools last).
- You want a visual, prioritized list of process redesigns to work through.

## What it does

1. **Interviews you first** — your business, your current architecture (tools, data, who does
   what), your pain points, your past decisions.
2. **Explores your processes** — finds shallow ones (that move complexity around instead of
   absorbing it), applies the deletion test, and spots where data and work leak.
3. **Produces an HTML report** — an overall verdict, a summary table, and **one fiche per
   candidate process**:
   - A verdict badge: 🟢 DEEP / 🟡 SHALLOW / 🔴 FRAGILE / ⚫ REMOVE
   - What actually happens, tagged FACT / INFERENCE / RECOMMENDATION — nothing invented
   - A depth check (interface vs complexity) and the deletion test
   - Frictions and risks rated LOW / MEDIUM / HIGH, with what to do
   - Current costs (time, money, cognitive load) and a value-vs-effort table
   - **3 redesign priorities maximum**, ranked MUST CHANGE / SHOULD CHANGE / NICE TO HAVE
   - What information is missing before deciding
   - A before/after visualisation per fiche
4. **Grills the candidates with you** — constraints, dependencies, what stays manual.
   Automation comes LAST, only after the process is deep and documented.

## Install

Copy the folder into your agent's skills directory (e.g. for Hermes):

```bash
cp -r huvi-business-architecture-optimizer ~/.hermes/skills/
```

## Example prompt

> My renovation business is losing leads between texts and calls, and I spend my evenings
> doing quotes. Audit my processes and tell me what to redesign.

## Core rules

- **You never automate chaos** — the golden rule. Deepening before automation, always.
- **The deletion test** — if removing a process just moves the complexity elsewhere, it's
  shallow: redesign or remove it.
- **The business's own language names the seams** — we use your words, not generic labels.
- **Facts, inferences and recommendations are never mixed** — if there is no trace of
  something, we say so instead of guessing.

## License

MIT. Created by [HUVI Optimisation](https://huvioptimisation.com).
