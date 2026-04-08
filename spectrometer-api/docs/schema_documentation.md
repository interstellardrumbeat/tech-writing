# Spectrometer Measurement Schema Documentation

This document provides a reference for the `measurement_schema.json` used in the **IFS 125HR Bruker Spectrometer API** project.  
It explains each field, its type, whether it is required, and its purpose.

## Top-level fields

| Field              | Type    | Required | Format | Example | Description |
|-------------------|--------|---------|--------|---------|-------------|
| experiment_id      | string | Yes     | String | `EXP-2026-03-21-001` | Unique identifier for the experiment. |
| instrument         | object | Yes     | Object | `{...}` | Details of the instrument used. |
| operator           | object | Yes     | Object | `{...}` | Information about the person running the experiment. |
| measurement        | object | Yes     | Object | `{...}` | Metadata about the measurement session. |
| scan_parameters    | object | Yes     | Object | `{...}` | Settings used for the scan. |
| spectrum           | object | Yes     | Object | `{...}` | Information about the recorded spectrum. |

---

## Nested objects

### `instrument`

| Field              | Type    | Required | Format | Example | Description |
|-------------------|--------|---------|--------|---------|-------------|
| name               | string | Yes     | String | `IFS 125HR` | Model name of the instrument. |
| manufacturer       | string | Yes     | String | `Bruker` | Manufacturer of the instrument. |
| resolution_cm-1    | number | Yes     | Float  | `0.001` | Spectral resolution in cm⁻¹. |

### `operator`

| Field              | Type    | Required | Format | Example | Description |
|-------------------|--------|---------|--------|---------|-------------|
| name               | string | Yes     | String | `Dr. Domenico Prudenzano` | Name of the operator. |
| lab                | string | Yes     | String | `DrumBeat Spectroscopy Lab` | Laboratory where the experiment was conducted. |

### `measurement`

| Field              | Type       | Required | Format | Example | Description |
|-------------------|-----------|---------|--------|---------|-------------|
| date               | string    | Yes     | ISO 8601 | `2026-03-21T10:15:00Z` | Date and time of measurement in ISO 8601 format. |
| location           | string    | Yes     | String | `Munich` | Location of the experiment. |
| temperature_C      | number    | Yes     | Float  | `18.4` | Ambient temperature in °C. |
| pressure_hPa       | number    | Yes     | Float  | `1012.3` | Ambient pressure in hPa. |

### `scan_parameters`

| Field              | Type     | Required | Format | Example | Description |
|-------------------|---------|---------|--------|---------|-------------|
| number_of_scans    | integer | Yes     | Integer | `128` | Number of interferometer scans. |
| scan_velocity_kHz  | number  | Yes      | Float  | `10` | Velocity of the scan in kHz. |
| apodization        | string  | Yes     | String | `Happ-Genzel` | Apodization function used (e.g., "Happ-Genzel"). |

### `spectrum`

| Field                    | Type   | Required | Format | Example | Description |
|---------------------------|-------|---------|--------|---------|-------------|
| wavenumber_range_cm-1     | array | Yes     | Array[2] numbers | `[4100, 4500]` | Range of wavenumbers [min, max] in cm⁻¹. |
| data_file                 | string| Yes     | String | `spectra/exp_20260321_001.dat` | Path to the spectrum data file. |

---

## Notes

- **Required fields** must be present in every JSON instance.  
- Nested objects reflect **real scientific data structures** used in our own spectrometer measurement software.  
- This schema can be used for **validation, API documentation, or automated data processing**.
