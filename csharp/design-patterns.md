# C# — design patterns (L1 lang)

rev: 2026-08-26
pin: `guiders-style@v1`
see: `../core/principles.md` (OOA&D, SOLID, DRY, KISS)

Language-aware **how** for org C#. Project canon wins on product UI/rules.

## OOA&D → C# shapes

- **Entity / role** → `sealed class` or `record` with clear name (`ForgeOrgMemberRow`, not `Data`).
- **Facade** → static or small service class; no 400-line «page builder» methods.
- **Port** → `interface` at boundary; infra implements in outer ring.
- **Value** → `record` (positional or property) — equality by value, immutable when possible.
- **`partial`** — **narrow case only** (see below); FileLines warn → OOA&D first, not dotted peels.

## When `partial` is OK (narrow)

`partial` уместен, когда есть **явная граница внедрения**, а не когда файл «слишком длинный»:

1. **Generated injection point** — source generator / designer / `.g.cs` вставляет код в **один** тип; руками правим только разрешённый `partial` слой.
2. **Framework / client split** — фреймворк даёт **базовый слой** (логика, контракт, sealed core); клиентский код живёт в `partial`, **не трогая** базовую логику фреймворка.

Если границы нет — это не `partial`, это сигнал к **новому типу** (OOA&D).

## When `partial` is wrong

- **Metric peel:** `TypeName.Something.cs` ради `file_lines` / SoftFL — `partial ≠ split`.
- **Partial family:** много dotted partials без framework/gen boundary (`partial_family` gate).
- **Fake seam:** ещё один `Foo.Bar.cs` вместо extract class / polymorphism / facade.

Depth: `playbook-ooad-agent-operational-v1.md` · habitat `quality` domain (`partial_family` tooth).

## Composition over inheritance

- Prefer **interface + DI** over deep `BaseController` / `BaseService` trees.
- **Extension methods** for cross-cutting utilities on narrow types — not a fat base class.
- **`record`** for DTOs, view models, wire JSON — not inheritance for data carrying.

## SOLID in practice

- **SRP** — one file/type per responsibility when file_lines warn fires.
- **OCP** — new behavior → new type or strategy; avoid editing giant switch unless registry/plugin model exists.
- **DIP** — domain/core does not reference ASP.NET, MCP host, or DB drivers directly.

## DRY / KISS

- Shared wire shapes — one record, reused; no copy-paste JSON anonymous objects across handlers.
- Three similar lines beat premature abstraction.

## Don't

- God class «because it's the host».
- Public inheritance for code reuse only.
- Static mutable singletons for «convenience» across features.

## Gates

- Same as `writing-surface.md`: `dotnet build` / `dotnet test` on touched projects.
