# Pure.Chart.RichRelationalModel.Abstractions

Combined chart domain-model and relational-model interfaces for the **Pure** ecosystem.

[![.NET build & test](https://github.com/kudima03/Pure.Chart.RichRelationalModel.Abstractions/actions/workflows/build-and-test.yml/badge.svg?branch=main)](https://github.com/kudima03/Pure.Chart.RichRelationalModel.Abstractions/actions/workflows/build-and-test.yml)
[![Build and Deploy](https://github.com/kudima03/Pure.Chart.RichRelationalModel.Abstractions/actions/workflows/publish-nuget.yml/badge.svg?branch=main)](https://github.com/kudima03/Pure.Chart.RichRelationalModel.Abstractions/actions/workflows/publish-nuget.yml)
[![NuGet](https://img.shields.io/nuget/v/Pure.Chart.RichRelationalModel.Abstractions)](https://www.nuget.org/packages/Pure.Chart.RichRelationalModel.Abstractions)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## Overview

`Pure.Chart.RichRelationalModel.Abstractions` defines four interfaces that each merge a chart
domain-model interface (navigation properties, human-readable semantics) with its relational-model
counterpart (identity via `IGuid`, foreign-key columns). The result is a *rich* view suitable for
EF Core entity types or any persistence layer that needs both navigation and flat relational
identity on the same object.

## Interfaces

| Interface | Extends | Description |
|---|---|---|
| `IChartRichRelationalModel` | `IChart`, `IChartRelationalModel` | Chart entity with title, description, type navigation, axis navigations, series collection, plus `Id`, `TypeId`, `XAxisId`, `YAxisId` FK columns |
| `IAxisRichRelationalModel` | `IAxis`, `IAxisRelationalModel` | Axis entity with `Legend` property plus `Id` |
| `IChartSeriesRichRelationalModel` | `IChartSeries`, `IChartSeriesRelationalModel` | Chart series entity with legend, axis-source properties, plus `Id` and `ChartId` FK |
| `IChartTypeRichRelationalModel` | `IChartType`, `IChartTypeRelationalModel` | Chart-type entity with `Name` property plus `Id` |

All interfaces live in the `Pure.Chart.RichRelationalModel.Abstractions` namespace.

## Design Principles

- **Composition over duplication** — each interface inherits the full contract of both its
  domain-model and relational-model parents; no properties are redefined.
- **Immutable by contract** — all inherited properties are read-only (`get`-only), enforced by the
  parent interfaces from `Pure.Chart.Model.Abstractions` and `Pure.Chart.RelationalModel.Abstractions`.
- **AOT-compatible** — no reflection or dynamic dispatch; safe for Native AOT publishing.

## Dependencies

- [`Pure.Chart.Model.Abstractions`](https://github.com/kudima03/Pure.Chart.Model.Abstractions/tree/0.1.0-preview.1.0.0) —
  chart domain-model interfaces (`IChart`, `IAxis`, `IChartSeries`, `IChartType`) with semantic
  navigation properties
- [`Pure.Chart.RelationalModel.Abstractions`](https://github.com/kudima03/Pure.Chart.RelationalModel.Abstractions/tree/0.1.0-preview.6.0.0) —
  relational-model interfaces that add `IGuid` identity and foreign-key columns to each chart
  entity

## Target Frameworks

- .NET 7
- .NET 8
- .NET 9
- .NET 10

## Installation

```shell
dotnet add package Pure.Chart.RichRelationalModel.Abstractions
```

## Usage

```csharp
using Pure.Chart.RichRelationalModel.Abstractions;

// Implement on an EF Core entity to satisfy both domain and persistence contracts.
public class ChartEntity : IChartRichRelationalModel
{
    public IGuid Id { get; init; } = default!;
    public IGuid TypeId { get; init; } = default!;
    public IGuid XAxisId { get; init; } = default!;
    public IGuid YAxisId { get; init; } = default!;
    public IString Title { get; init; } = default!;
    public IString Description { get; init; } = default!;
    public IChartType Type { get; init; } = default!;
    public IAxis XAxis { get; init; } = default!;
    public IAxis YAxis { get; init; } = default!;
    public IEnumerable<IChartSeries> Series { get; init; } = [];
}
```
