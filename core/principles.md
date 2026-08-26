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

## When to go deeper

| Need | KB / tool |
|------|-----------|
| OOA&D playbook | `playbook-ooad-agent-operational-v1.md` |
| C# mechanics | `guiders-style/csharp/design-patterns.md` |
| Language habits | `guiders-style/{lang}/writing-surface.md` |
| This repo | `{scm}/.cdp/canon.md` |
