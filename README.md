# guiders-style

Org writing surfaces (L1) for CDP writing canon stack ([CDP-ADR-0207](https://github.com/AI-Guiders/cdp-mcp/blob/main/docs/adr/CDP-ADR-0207-writing-canon-layers.md)).

License: [CC BY-SA 4.0](LICENSE).

Pin in project: `.cdp/project.toml` → `org_style = "guiders-style@v1"`.

Host path: `cdp-mcp.toml` → `[canon].guiders_style_root`.

## Layout

```text
pins/v1.toml      # @v1 manifest (traceability)
core/
  principles.md   # OOA&D, KISS, DRY, SOLID — org operational (~600 tok route)
csharp/
  writing-surface.md
  design-patterns.md
  cli.md              # argv parsing — Ookii default; no hand-roll loops
python/           # (future)
powershell/       # (future)
```
