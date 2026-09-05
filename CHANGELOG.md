# Changelog

All notable changes to Pure.Chart.RichRelationalModel.Abstractions are documented here.

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

---

## [0.1.0-preview.4.0.0] — 2026-04-26

- Maintenance release: bumped the `Pure.Chart.RelationalModel.Abstractions` dependency
  to `0.1.0-preview.6.0.0`; package validation baseline updated.

## [0.1.0-preview.3.0.0] — 2026-04-19

### Changed

- **`ISeriesRichRelationalModel`** renamed to **`IChartSeriesRichRelationalModel`**,
  now extending `IChartSeries` and `IChartSeriesRelationalModel` (previously `ISeries`
  and `ISeriesRelationalModel`), following the corresponding rename in the upstream
  `Pure.Chart.Model.Abstractions` and `Pure.Chart.RelationalModel.Abstractions`
  packages.
- Bumped `Pure.Chart.RelationalModel.Abstractions` to `0.1.0-preview.5.0.0` and
  `Pure.Chart.Model.Abstractions` to `0.1.0-preview.1.0.0`.

### Removed

- **`ISeriesRichRelationalModel`** (replaced by `IChartSeriesRichRelationalModel`).

## [0.1.0-preview.2.1.0] — 2026-02-27

- Maintenance release: bumped the `Pure.Chart.RelationalModel.Abstractions` dependency
  to `0.1.0-preview.4.1.0`.

## [0.1.0-preview.2.0.0] — 2026-02-16

- Maintenance release: bumped the `Pure.Chart.RelationalModel.Abstractions` dependency
  to `0.1.0-preview.4.0.0`; package validation baseline updated.

## [0.1.0-preview.1.0.0] — 2026-02-14

- Maintenance release: bumped the `Pure.Chart.RelationalModel.Abstractions` dependency
  to `0.1.0-preview.3.0.0`; package validation baseline updated.

## [0.1.0-preview.0.2.0] — 2026-02-12

### Fixed

- Multi-targeting corrected to `net7.0`, `net8.0`, `net9.0`, and `net10.0` (the
  project previously listed `net10.0` four times instead of the intended target
  frameworks).

## [0.1.0-preview.0.1.0] — 2026-02-12

### Added

- Initial release.
- **`IChartRichRelationalModel`** — combines `IChart` and `IChartRelationalModel`.
- **`IAxisRichRelationalModel`** — combines `IAxis` and `IAxisRelationalModel`.
- **`ISeriesRichRelationalModel`** — combines `ISeries` and `ISeriesRelationalModel`.
- **`IChartTypeRichRelationalModel`** — combines `IChartType` and
  `IChartTypeRelationalModel`.
- References to `Pure.Chart.Model.Abstractions` and
  `Pure.Chart.RelationalModel.Abstractions`.
