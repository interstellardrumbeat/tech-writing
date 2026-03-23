# Spectrometer Measurements - JSON Format

This project defines a **JSON schema** for storing metadata from FTIR spectrometer measurements.  
It describes the structure and validation rules for measurement metadata, including experiment identifiers, instrument details, scan parameters, environmental conditions, and spectrum data.

## Files

| File                       | Description                                |
| -------------------------- | ------------------------------------------ |
| `measurement_schema.json`  | JSON schema defining the data structure    |
| `measurement_example.json` | Example measurement file that follows the schema |
| `schema_documentation.md`      | Documentation of all the schema fields |

## Example JSON

```
{
  "experiment_id": "EXP-2026-03-21-001",
  "instrument": {
    "name": "IFS 125HR",
    "manufacturer": "Bruker"
  },
  "operator": {
    "name": "Dr. Domenico Prudenzano"
  },
  "measurement": {
    "date": "2026-03-21T10:15:00Z",
    "temperature_C": 18.4
  },
  "scan_parameters": {
    "number_of_scans": 128,
    "apodization": "Happ-Genzel"
  },
  "spectrum": {
    "wavenumber_range_cm-1": [4100, 4500]
  }
}
```
The full JSON file is available in measurement_example.json for validation or download.

## Validation

You can validate the JSON file against the schema using standard JSON Schema validators.

Example using `ajv-cli`:
```
npm install -g ajv-cli
ajv validate -s measurement_schema.json -d measurement_example.json
```
If the JSON file conforms to the schema, you will see `measurement_example.json valid`.

>NOTE: Requires [Node.js](https://nodejs.org). Works on Linux, macOS, and Windows.

## Documentation

See `schema_documentation.md` for detailed descriptions of each field.
