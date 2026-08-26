# Org design principles (L1 core)

rev: 2026-08-26
pin: `guiders-style@v1`
budget: ~600 tokens in route · depth via KB on demand

Operational defaults for agents **before first edit**. Not a textbook — pointers for when stuck.

## OOA&D (model before code)

- Name **nouns** (entities, roles, value objects) and **verbs** (use cases) before growing procedures.
- **One job per type** — facades/router thin; state owned once (no hidden shared mutable soup).
- File/method pressure → **OOA&D pass** (nouns → types). `partial` class: **strong OK** = gen/designer injection; framework boundary = **virtual/override**, not partial.
- Depth: `read_knowledge_file` → `playbook-ooad-agent-operational-v1.md` (software.authoring).

## KISS

- Simplest design that meets the requirement today. No speculative layers «на будущее».

## DRY

- One SSOT per fact/rule. Duplicate only when decoupling cost clearly wins.

## SOLID (checklist, not ceremony)

- **S** — one reason to change per type at this layer.
- **O/L** — extend via new types/composition; avoid fragile base-class hierarchies.
- **I** — small interfaces; split fat interfaces.
- **D** — depend on abstractions at boundaries (ports), not concrete infra in domain core.
- Depth: KB worlds `software-dotnet-csharp` (explore phase), not every edit.

## Composition over inheritance

- Default **has-a** + interfaces/protocols. Inheritance only for true subtype polymorphism.

## YAGNI

- Vertical slice that ships; no «v1 stub» unless explicitly requested.

## Proven building blocks (don't invent the bicycle)

- **General rule:** solved problem + **compatible, maintained library** (or platform API) → **use it**, not a hand-rolled «велосипед» — CLI, JSON, HTTP, logging, crypto, parsing, retries, anything with a stable ecosystem answer.
- **.NET stack:** prefer packages that target **net10** (or multi-target including net10). Older TFM-only lib is **fine** if it runs on our runtime without hacks — compatibility beats purism.
- **Org picks** (`guiders-style` lang files, `.cdp/canon.md`, dogfood) = **shortcuts**, not a cage — check them so we don't rediscover the same wheel; **not mandatory** if something else is clearly better.
- **Better / newer is welcome:** agent, NuGet, upstream docs, or a sibling repo may surface a stronger package — take it when justified (maintained, compatible, license OK). Brief *why this over default* in PR/README; **update the org pick** when the new choice sticks.
- **Hand-roll only when:** no acceptable lib, hard constraint (license, trim/AOT, air-gap, toxic transitive deps), or genuinely domain-specific logic.
- New dependency → pinned version, license OK. Lang files (e.g. `csharp/cli.md`) record current defaults — living list, not frozen law.

## When to go deeper

| Need | KB / tool |
|------|-----------|
| OOA&D playbook | `playbook-ooad-agent-operational-v1.md` |
| C# mechanics | `guiders-style/csharp/design-patterns.md` |
| C# CLI / argv | `guiders-style/csharp/cli.md` |
| Language habits | `guiders-style/{lang}/writing-surface.md` |
| This repo | `{scm}/.cdp/canon.md` |
