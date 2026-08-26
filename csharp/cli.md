# C# — CLI argument parsing (L1)

rev: 2026-08-26
pin: `guiders-style@v1`
see: `../core/principles.md` (proven building blocks) · `writing-surface.md` · dogfood: `AIGuiders.DotnetTools.PublishFixedTarget`

## Rule

**Do not hand-roll `Environment.GetCommandLineArgs()` loops** — CLI parsing is a solved problem; see org principle *Proven building blocks* in `core/principles.md`.

## Default (org)

**[Ookii.CommandLine](https://www.nuget.org/packages/Ookii.CommandLine) 5.x**

- Console / `dotnet tool`: `[GeneratedParser]` + `partial class` + `Args.Parse(args)` (see `aid-publish` in `AIGuiders.DotnetTools`).
- GNU-style long options (`--wave`, `--dry-run`): `[ParseOptions(Mode = ParsingMode.LongShort, ArgumentNameTransform = NameTransform.DashCase)]` on the args type.
- Positional command first (`Position = 0`), then named options.

## `dotnet script` (.csx)

Acceptable when the script stays small; still use Ookii, not a manual loop:

```csharp
#nullable enable
#r "nuget: Ookii.CommandLine, 5.0.0"
using Ookii.CommandLine;

[ParseOptions(Mode = ParsingMode.LongShort, ArgumentNameTransform = NameTransform.DashCase)]
class CliArgs { /* [CommandLineArgument] properties */ }

static string[] ScriptUserArgs() {
    var raw = Environment.GetCommandLineArgs();
    var i = Array.FindIndex(raw, s => s.EndsWith(".csx", StringComparison.OrdinalIgnoreCase));
    return (i >= 0 ? raw.Skip(i + 1) : raw.Skip(1)).ToArray();
}

var cli = CommandLineParser.Parse<CliArgs>(ScriptUserArgs());
if (cli is null) return 1;
```

When the CLI gains subcommands, validation, or tests → **promote to a small `Exe` project** (same Ookii type; drop `#r`).

## Alternatives (explicit opt-in)

| Library | When |
|---------|------|
| **System.CommandLine** | Deep subcommand trees, shell completions (`dotnet-suggest`); heavier than Ookii for flat tools |
| **McMaster.Extensions.CommandLineUtils** | Legacy scripts only — do not start new tools on it |

Do **not** add the old **CommandLineParser** NuGet (different package/API; confuses search and reviews).

## Don't

- `for` loops over argv with `if (a == "--foo")` / `continue` (fragile; no `--help`)
- Mixing positional commands and unconsumed flag values without a parser
- Copy-pasting argv helpers across repos — one args type per entrypoint

## Gates

- `--help` / invalid args → non-zero exit, usage on stderr or stdout per tool convention
- Smoke the real argv shape in CI or a one-liner doc comment at top of `Program.cs` / `.csx`
