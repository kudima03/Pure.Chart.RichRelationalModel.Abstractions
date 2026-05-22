# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

All `dotnet` commands must be run from the `./src` directory.

```bash
dotnet restore
dotnet build --no-restore -warnaserror
dotnet format --verify-no-changes             # check code style (CI enforces this)
dotnet format && csharpier format .           # auto-fix code style
dotnet pack --configuration Release -p:PackageVersion=<version> --output .
```

There are no test projects in this repository — the CI pipeline only builds and checks formatting.

## Architecture

This is an **interfaces-only NuGet library** — no implementations, no tests, no runtime
dependencies beyond its two Pure sibling packages. Every file defines exactly one interface.

**Purpose:** each of the four interfaces merges a chart domain-model interface (from
`Pure.Chart.Model.Abstractions`) with its relational-model counterpart (from
`Pure.Chart.RelationalModel.Abstractions`). This "rich relational model" pattern is used by
EF Core entity types and persistence layers that need both semantic navigation properties and
flat relational identity (`IGuid` PK + FK columns) on the same object.

**Composition hierarchy:**

```
IChartRichRelationalModel     : IChart, IChartRelationalModel
IAxisRichRelationalModel      : IAxis, IAxisRelationalModel
IChartSeriesRichRelationalModel : IChartSeries, IChartSeriesRelationalModel
IChartTypeRichRelationalModel : IChartType, IChartTypeRelationalModel
```

**Multi-targeting:** net7.0, net8.0, net9.0, net10.0. All interfaces must remain AOT-compatible
(`IsAotCompatible = true`).

**Package validation:** `EnablePackageValidation = true` with
`PackageValidationBaselineVersion = 0.1.0-preview.4.0.0`. Breaking changes fail the build.

**Publishing:** triggered by pushing a semver tag (e.g. `0.1.0-preview.5.0.0`). The tag becomes
the `PackageVersion`. Packages are published to both GitHub Packages and NuGet.org.

## Code Style

Enforced via `.editorconfig` and `dotnet format --verify-no-changes` + `csharpier check .` in CI:

- **No `var`** — always use explicit types (`csharp_style_var_*` = false).
- **File-scoped namespaces** — `namespace Foo.Bar;` not `namespace Foo.Bar { }`.
- **`using` directives outside namespace** — `csharp_using_directive_placement = outside_namespace`.
- **No expression-bodied methods or constructors** — only properties, indexers, accessors, and
  lambdas may use expression bodies.
- **No implicit object creation** — `new Foo()` not `new()` when the type is apparent.
- **Max line length: 90 characters.**
- **Private fields:** `_camelCase` (underscore prefix).
- **No public/protected instance fields** — use properties; violations are errors.
- Suppressions in effect: CA1716 (reserved identifiers), CA1859 (use concrete types),
  CA1305 (culture-specific formatting), CA1720 (type names in identifiers).

## Commit Messages

Do not mention Claude or AI assistance in commit messages.
