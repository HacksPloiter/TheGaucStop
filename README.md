# The Gauc Stop - An end-to-end cloud data warehouse and analytics solution

## Introduction
This project implements a complete cloud data warehouse solution designed to store, manage, and analyze business data. The workflow was developed using Oracle Cloud Infrastructure, Apache Hop, and the ETL process automates the extraction, transformation, and loading of data into both dimension tables and fact tables.

## Key objectives:
- Build a robust dimensional model.
- Automate data ingestion and transformation.
- Enable analytical queries for reporting and decision-making.

## Technologies Used
-   **Apache Hop**  – An open source ETL orchestration tool
-   **Oracle Cloud Infrastructure** - Cloud data warehouse platform
-   **Oracle Autonomous Database**  – Data warehouse storage
-   **SQL**  – Data manipulation and schema creation
-   **Star Schema**  – Dimensional modeling technique
-   **Tableau** - Analytics solution
-   **Python** - Data filtering and transformation logic in Apache Hop.

## Architecture & Design
### 1. Dimensional Modeling
The data warehouse follows a  **star schema**  consisting of:
-   **Dimension Tables**  – Containing descriptive attributes (e.g.,  Dim_Cust,  Dim_Prod,  Dim_Date, etc.).
-   **Fact Tables**  – Containing quantitative business data linked via foreign keys to dimensions.

Here is the ER diagram:

Below is the Data Model:

### 2. ETL Workflow
- **Tool:**  [Apache Hop](https://hop.apache.org/)
- **Automation:**  The ETL pipeline is designed to run automatically, extracting raw data from source systems, transforming it to match the dimensional model, and loading it into the data warehouse.
- **Flow Steps:**
    1.  **Extract**  – Pull data from sources files such as excel spreadsheets.
    2.  **Transform**  – Clean, format, and enrich data; create surrogate keys; manage slowly changing dimensions.
    3. **Load**  – Populate dimension tables first, then fact tables.
    4.  **Scheduling**  – Configured for regular execution to keep data updated.

ETL Flow:

### 3. Analytics
Once the data is in the warehouse, an analytics layer enables reporting and business insights using Tableau:
-   **Data Access**  – Analysts connect directly to the warehouse using BI tools.
-   **BI Integration**  – Connectivity with tools Tableau for interactive dashboards.
-   **Pre-Aggregated Views**  – Materialized views or summary tables created to speed up common analytical queries.
-   **KPIs & Metrics**  – Standardized measures (e.g., sales revenue, customer churn rate, average order value) defined within the warehouse for consistent reporting.
-   **Ad Hoc Analysis**  – The schema supports flexible slicing and dicing of facts by various dimensions (e.g., sales by product, by region, by time period).

Tableau Dashboard:

## Challenges

1.  Connection authentication was failing on first connection from Apache Hop to the data warehouse. I used “launchctl setenv TNS_ADMIN /Applications/instantclient/network/admin” command to set the correct environment vairables as I was using alias to tns_names.ora file.
2. The data type in the data warehouse tables across tables of key fields were not same. For example, the data type of DATE was character in fact table, whereas it was number in date dimension. I changed the data type to make it uniform.
3.  The date values in the fact table had leading zeroes whereas the date in the dimension table didn’t have leading zeroes. I ran a SQL script, to correct these inconsistencies.
4.  Tableau after fetching the data types was assigning wrong data type for some of the columns. Corrected.
5.  While creating visualization, for the date out of range of actual sales, Tableau was considering them as NULL dates. This happened because the populated date in dimension table had extra dates beyond and before the dates of sales. To debug this, I used date filter in the visualization.

## Key Takeaways
1.  **Comprehensive Cloud Data Warehouse and Analytics Solution** – Implemented a star schema with dimension and fact tables on oracle cloud infrastructure, designed for scalable analytical querying and business intelligence.
3.  **Automated ETL with Apache Hop** – Developed fully orchestrated extraction, transformation, and loading process, including incremental loads, error handling, slowly changing dimensions (SCD) handling, and scheduling for continuous updates.
4.  **Clear Structure & Expandability** – Organized project folders, reusable pipelines, and room for future enhancements like real-time streaming and additional data sources.
