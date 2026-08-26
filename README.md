# guiders-style

Org writing surfaces (L1) for CDP writing canon stack ([CDP-ADR-0207](https://github.com/AI-Guiders/cdp-mcp/blob/main/docs/adr/CDP-ADR-0207-writing-canon-layers.md)).

Pin in project: `.cdp/project.toml` → `org_style = "guiders-style@v1"`.

Host path: `cdp-mcp.toml` → `[canon].guiders_style_root`.

## Layout

```text
core/           # cross-lang (future)
csharp/         # C# / .NET Human View + MCP
python/         # (future)
```

## csharp

- `writing-surface.md` — operational slice (~800 token budget in route)
