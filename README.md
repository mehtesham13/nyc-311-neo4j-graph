# NYC 311 Service Requests as a Neo4j Graph

Which agencies, boroughs and complaint types drive NYC's 311 workload, and how fast do requests get closed? This project loads NYC 311 data into Neo4j and answers those questions with Cypher.

## Data

305,703 NYC 311 service requests from November–December 2025 ([NYC Open Data](https://data.cityofnewyork.us/Social-Services/311-Service-Requests-from-2010-to-Present/erm2-nwe9)).

## Graph model

Five node types: `Request`, `Agency`, `Complaint`, `Borough`, `Location`.

```
(:Request)-[:BY_AGENCY]->(:Agency)
(:Request)-[:HAS_COMPLAINT]->(:Complaint)
(:Request)-[:IN_BOROUGH]->(:Borough)
(:Borough)-[:LOCATED_AT]->(:Location)
```

A graph fits this data because most questions are about links between entities. "Which agencies handle noise complaints in Queens" is a short traversal here, where a relational schema would need several joins.

## Method

- Loaded the CSV with `LOAD CSV` and `MERGE` so each agency, borough and complaint type exists once
- Converted text timestamps to native `datetime` values with APOC
- Added a `resolutionHours` property (closed date minus created date)
- Flagged noise complaints with conditional logic for comparison across boroughs

## Findings

- **NYPD** handled the most requests, over 140,000 in two months.
- **Queens** closed requests fastest, averaging 24.93 hours.
- **Manhattan** had the highest share of noise complaints relative to its total requests (2.85%).

## Files

| File | Contents |
|---|---|
| `cypher/01_node_creation.cypher` | Cypher for loading the CSV and creating nodes and relationships |
| `cypher/02_cleaning_and_transformation.cypher` | Cypher for null handling, date conversion and feature engineering |
| `NYC_311_Graph_Database_Project_Presentation.pdf` | Slides with the data model and results |

Run the scripts in order in Neo4j Browser or `cypher-shell`, with the APOC plugin installed.

## Team

Muhammad Ehtesham, Yunus Emre Paksoy, Nobukhosi Sibanda
