# Security Force Monitor: Senior Developer Code Challenge

Hello and welcome to Security Force Monitor's (SFM) code challenge for Senior Developers!

We're asking you to do a data wrangling and tooling task. You'll be creating a tool that transforms SFM's tabular data about security force organizational structures into graph that analysed and visualised.

### Task

The data provided in `data/202106251341-HEAD-Mali-Backup-slime.xlsx` describes the security and defences forces of Mali. 

The task is as follows:

- Create a command line tool that can construct a directed graph from the given data and show the parentage and children of the unit called `32 Régiment d’Infanterie Motorisée` and output it in GraphML format.

Your application should be:

- Written in Python
- Make use of the [NetworkX](https://networkx.org/) library
- be called from the default macOS `zsh` terminal 

The command should be executed from the command line in the following manner:

```
graph --input data/202106251341-HEAD-Mali-Backup-slim.tsv \ 
      --unit "32 Régiment d’Infanterie Motorisée" \
      --traverse-direction "both"
      --output output/32_rim_graph.grapml
```
 
The expected output from this command, in GraphML format, is provided in `output/324_cd_command_chain_raw.graphml`. 

To assist you, we have provided a laid out and formatted versions of the output are provided in `examples/324_cdm_command_chain_formatted.graphml` and `examples/324_cdm_command_chain_formatted.pdf`. We laid out the graph using [yEd Graph Editor](https://www.yworks.com/products/yed).


## Data model

Security Force Monitor data is stored in a flat representation of a directed acyclic graph. It describes a set of hierarchical relationships between units - like companies, battalions, brigades, divisions. 

### Fields

Position|Name|Decsription
---|---|---
1|`unit:id:admin`|Unit's unique identifier (UUID v4 format)|
2|`unit:name`|Name of the unit|
3|`unit:classification`|Security force branch(es) that unit is part of (semi-colon separated entries)|
4|`unit:relation_type`|Type of relationship between units ("child", "member")|
5|`unit:related_unit_id:admin`|Unique id of related unit (UUID v4 format)|
6|`unit:related_unit`|Name of the related unit|
7|`unit:related_unit_class`|Nature of authority in relationship ("command", "informal")
8|`unit:related_unit_first_cited_date`|full or partial date when the relationship was first observed, or strarted|
9|`unit:related_unit_first_cited_date_start`|whether the date on which relationsip was first observed is an actual start date ("Y"), or just the earliest observation ("N"|
10|`unit:related_unit_last_cited_date`|full or partial date when the relationship was most recently observed, or ended|
11|`unit:related_unit_open`|whether the date the relationship between units is open-ended ("Y") or not ("N","E")|

We have published extended documentation on the [unit entity and fieldset](https://help.securityforcemonitor.org/en/latest/units.html) in our Research Handbook.

### Graph construction rules for SFM data

To transform the tabular data into a graph, consider the following rules:

- The complete universe of nodes is described the unique list of values in `unit:id:admin`
- Each row describes an edge.
- Nodes may be linked with multiple edges simultaneously or over time.
- The source or parent node of a node is described in `unit:related_unit_id:admin`, and the target or child node is described in `unit:id:admin`
- The duration over which the edge is valid is described with an earlier date (`unit:related_unit_first_cited_date`) and a later date (`unit:related_unit_last_cited_date`).

## Contents of this repository

```
.
├── README.md
├── data
│   └── 202106251341-HEAD-Mali-Backup-slim.tsv
├── examples
│   ├── 324_cdm_command_chain_formatted.graphml
│   ├── 324_cdm_command_chain_formatted.pdf
│   └── 324_cdm_command_chain_raw.graphml.graphml
└── output

```