# C# / .NET — org writing surface (L1)

rev: 2026-08-26
pin: `guiders-style@v1`

Normative ADRs stay in product repos. This file = cross-repo C# habits for agents.

See also: `design-patterns.md` (OOA&D/SOLID → C# mechanics) · `../core/principles.md` (org principles).

## Do

- Nullable enabled; annotate public API; `async` + `ConfigureAwait` policy per host (CDP tests: omit ConfigureAwait)
- `sealed` records for view models and DTO wire shapes
- XML docs on public plugin surfaces; internal = minimal
- Tests: xunit; name `Method_Scenario_Expectation`
- Human View (Forge): Kit + Razor — see `agent-forge/.cdp/canon.md`
- Dependencies: **proven libs over hand-roll** — `../core/principles.md`; area picks e.g. `cli.md` (Ookii.CommandLine)

## Don't

- String-built HTML tables in C# for operator UI (ForgeHtml page builders)
- `async void` except UI event handlers
- Public API without nullable contract review

## Gates

- `dotnet build` / `dotnet test` on touched projects before ship
