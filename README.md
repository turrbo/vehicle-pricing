# Vehicle Pricing

Analyze vehicle pricing and determine deal quality by comparing against market data from CarGurus, AutoTempest, Cars.com, KBB, Edmunds, and other platforms. Use when the user asks to: (1) Check if a vehicle listing is a good deal, (2) Find fair market price for a specific year/make/model/trim/mileage, (3) Evaluate a vehicle listing URL, (4) Determine what a dealer should pay wholesale to resell at profit, (5) Compare vehicle prices across platforms, (6) Get depreciation forecast or cost of ownership, (7) Check recalls on a vehicle, (8) Value a salvage or rebuilt title vehicle, or any vehicle pricing, valuation, or deal analysis task.

## What this repo contains

- `SKILL.md` — the primary agent skill definition and workflow.
- `references/` — supporting playbooks, platform rules, examples, or data used by the skill.

## Reference material

- `references/deal-analysis.md`
- `references/pricing-sources.md`
- `references/additional-analysis.md`

## Installation

Copy this repository or the skill directory into your agent's skills directory, then load the skill by name when the task matches its use case.

```bash
# example
cp -R vehicle-pricing ~/.claude/skills/vehicle-pricing
```

## Repository layout

```text
references/
  additional-analysis.md
  deal-analysis.md
  pricing-sources.md
SKILL.md
```

## Notes

The root README summarizes the live repository contents. The complete operational instructions remain in `SKILL.md`.
