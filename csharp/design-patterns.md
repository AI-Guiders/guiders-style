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

## `partial` class (C#) — not Razor partial

Razor **view partials** (`Pages/Shared/*.cshtml`) — другой механизм; см. project canon (Kit). Здесь только C# `partial class`.

FileLines warn → **OOA&D first** (nouns → types), not dotted peels.

### OK (strong)

**Generated injection point** — source generator / designer / `.g.cs` вставляет в **один** тип; руками правим только разрешённый `partial` слой.

### Weak (discuss, не default)

Hand `partial` на **своём** типе — только **организация** одной class (team-owned файлы). Не seam. При росте → **новый тип** (OOA&D), не ещё `Foo.Bar.cs`.

### Framework extension — **не** `partial`

Граница с фреймворком → **inheritance + `abstract` / `virtual` / `override`** (или interfaces). Не `partial` на framework types; не «дописать» их класс.

```csharp
public partial class MyController : Controller  // partial = твоя организация
{
    public override IActionResult Index() { ... }  // расширение = override
}
```

### Wrong

- **Metric peel:** `TypeName.Something.cs` ради `file_lines` / SoftFL — `partial ≠ split`.
- **Partial family:** много dotted partials без gen boundary (`partial_family` gate).
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
