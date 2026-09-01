# huvi-business-architecture-optimizer

Audits a business's processes and proposes **deepening opportunities** — redesigns that turn
shallow processes into deep ones — presented as a visual HTML report, then grilled through
with the owner.

## When to use

- You feel your operations are heavy and you don't know where time and money leak.
- You want to prepare a process for automation the RIGHT way (structure first, tools last).
- You want a visual, prioritized list of process redesigns to work through.

## What it does

1. **Interviews you first** — your business, your current architecture (tools, data, who does
   what), your pain points, your past decisions.
2. **Explores your processes** — finds shallow ones (that move complexity around instead of
   absorbing it), applies the deletion test, and spots where data and work leak.
3. **Produces an HTML report** — one card per candidate: problem, solution, benefits,
   before/after diagram, recommendation strength (`Strong` / `Worth exploring` / `Speculative`)
   and a Top recommendation.
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

## License

MIT. Created by [HUVI Optimisation](https://huvioptimisation.com).
