# Security Force Monitor: Senior Developer Code Challenge

## Contents

```
.
├── README.md
├── output
│   ├── 324_cdm_command_chain_formatted.graphml
│   ├── 324_cdm_command_chain_formatted.pdf
│   └── 324_cdm_command_chain_raw.graphml
└── sources
    └── 202106251341-HEAD-Mali-Backup.xlsx

```

## Task

The data provided in the `ml_units` sheet of `output/202106251341-HEAD-Mali-Backup.xlsx` describes the security and defences forces of Mali. Construct a directed graph showing the parentage and children of the unit called `32 Régiment d’Infanterie Motorisée`. The expected output in GraphML format is provided in `output/324_cd_command_chain_raw.graphml`. Laid out and formatted versions of the output are provided in `output/324_cdm_command_chain_formatted.graphml` and  `output/324_cdm_command_chain_formatted.pdf`.

## Further information

 - Nodes are described in `unit:id:admin`, and their labels in `unit:name`.
 - The parent of a node is described in `unit:related_unit_id:admin`
