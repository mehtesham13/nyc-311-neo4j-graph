

## **NYC 311 Service Requests: Neo4j Graph Database Analysis**

### **Project Overview**

This project transforms a subset of the **NYC 311 Service Requests dataset** into a highly interconnected graph database using **Neo4j**. By moving away from traditional relational models, we explore the complex relationships between city agencies, complaint types, and geographical boroughs to discover patterns in urban service performance.

* **Dataset**: 305,703 rows of NYC 311 data (Nov 2025 – Dec 2025).


* **Core Technology**: Neo4j (Graph Storage), Cypher (Query Language), APOC (Data Transformation).



### **Why a Graph Database?**

Traditional relational joins become complex and inefficient when dealing with deeply interconnected city data. Using a graph model allows for:

* **Intuitive Modeling**: Directly representing how a **Request** is linked to an **Agency**, **Borough**, and **Complaint Type**.


* **High Performance**: Efficient traversals across different entities for relationship-heavy queries.


* **Flexible Schema**: Easy adaptation for future advanced urban analytics.



### **The Data Model**

The graph consists of five primary node entities:

* **Request**: The central event containing status and timestamps.


* **Agency**: The NYC department handling the request (e.g., NYPD, HPD, DSNY).


* **Complaint**: The specific issue type and descriptor.


* **Borough**: The geographical region (Manhattan, Brooklyn, etc.).


* **Location**: Precise spatial data including address and coordinates.



**Relationships**:

* `(:Request)-[:BY_AGENCY]->(:Agency)`
* `(:Request)-[:HAS_COMPLAINT]->(:Complaint)`
* `(:Request)-[:IN_BOROUGH]->(:Borough)`
* `(:Borough)-[:LOCATED_AT]->(:Location)`

### **Key Features & Analysis**

* **Data Transformation**: Leveraged **APOC** to convert string timestamps into native DateTime objects and engineered a `resolutionHours` feature for efficiency analysis.


* **Noise Analysis**: Implemented conditional logic to flag noise-related complaints, finding that **Manhattan** has the highest percentage of noise issues relative to total requests (2.85%).


* **Performance Benchmarking**: Analyzed average resolution times per borough, revealing that **Queens** has the fastest average resolution at **24.93 hours**.


* **Agency Workload**: Identified **NYPD** as the highest-volume agency, handling over **140,000 requests** in the analyzed period.



### **Repository Structure**

* `NODE CREATION.sql`: Cypher scripts for loading and merging data from CSV.
* `DATA CLEANSING and TRANSFORMATION.sql`: Scripts for handling null values and feature engineering.
* `QUERIES(AGGREGATIONS).sql`: Analytical queries for performance and distribution insights.
* `NYC_311_Graph_Database_Project_Presentation.pptx`: Detailed project overview and visualizations.

### **Contributors**

* **Muhammad Ehtesham** 


* Yunus Emre Paksoy 


* Nobukhosi Sibanda 



---
