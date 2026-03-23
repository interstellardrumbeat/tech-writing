# Spectrometer Measurement Schema Reference

This document provides a reference for the `measurement_schema.json` used in the Spectrometer-JSON project.  
It explains each field, its type, whether it is required, and its purpose.

---

## Top-level fields

| Field              | Type    | Required | Description |
|-------------------|--------|---------|-------------|
| experiment_id      | string | Yes     | Unique identifier for the experiment. |
| instrument         | object | Yes     | Details of the instrument used. |
| operator           | object | Yes     | Information about the person running the experiment. |
| measurement        | object | Yes     | Metadata about the measurement session. |
| scan_parameters    | object | Yes     | Settings used for the scan. |
| spectrum           | object | Yes     | Information about the recorded spectrum. |

---

## Nested objects

### `instrument`

| Field              | Type    | Required | Description |
|-------------------|--------|---------|-------------|
| name               | string | Yes     | Model name of the instrument. |
| manufacturer       | string | Yes     | Manufacturer of the instrument. |
| resolution_cm-1    | number | Yes     | Spectral resolution in cm⁻¹. |

### `operator`

| Field              | Type    | Required | Description |
|-------------------|--------|---------|-------------|
| name               | string | Yes     | Name of the operator. |
| lab                | string | Yes     | Laboratory where the experiment was conducted. |

### `measurement`

| Field              | Type       | Required | Description |
|-------------------|-----------|---------|-------------|
| date               | string    | Yes     | Date and time of measurement in ISO 8601 format. |
| location           | string    | Yes     | Location of the experiment. |
| temperature_C      | number    | Yes     | Ambient temperature in °C. |
| pressure_hPa       | number    | Yes     | Ambient pressure in hPa. |

### `scan_parameters`

| Field              | Type     | Required | Description |
|-------------------|---------|---------|-------------|
| number_of_scans    | integer | Yes     | Number of interferometer scans. |
| scan_velocity_kHz  | number  | No      | Velocity of the scan in kHz. |
| apodization        | string  | Yes     | Apodization function used (e.g., "Happ-Genzel"). |

### `spectrum`

| Field                    | Type   | Required | Description |
|---------------------------|-------|---------|-------------|
| wavenumber_range_cm-1     | array | Yes     | Range of wavenumbers [min, max] in cm⁻¹. |
| data_file                 | string| Yes     | Path to the spectrum data file. |

---

## Notes

- **Required fields** must be present in every JSON instance.  
- Nested objects reflect **real scientific data structures** used in our own spectrometer measurement software.  
- This schema can be used for **validation, API documentation, or automated data processing**.
