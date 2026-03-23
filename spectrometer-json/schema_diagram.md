# Measurements Data - Diagram 

This diagram shows the structure of the **Measurement JSON schema**. 

Measurement
├── experiment_id : string
├── instrument : object
│   ├── name : string
│   ├── manufacturer : string
│   └── resolution_cm-1 : number
├── operator : object
│   ├── name : string
│   └── lab : string
├── measurement : object
│   ├── date : string (ISO 8601)
│   ├── location : string
│   ├── temperature_C : number
│   └── pressure_hPa : number
├── scan_parameters : object
│   ├── number_of_scans : integer
│   ├── scan_velocity_kHz : number
│   └── apodization : string
└── spectrum : object
    ├── wavenumber_range_cm-1 : array[number, number]
    └── data_file : string
