# awesome-query-languages

A technical reference repository for Splunk Processing Language (SPL), Kusto Query Language (KQL), and Elasticsearch Query Language (ES|QL). This project serves as a syntax guide and implementation reference for security analysts and engineers working across multiple observability platforms.

## Repository Structure

The repository is divided into three primary directories, each dedicated to a specific query language and organized by functional intent.

### 1. [Full SPL Reference](./Full%20SPL%20Reference)
Documentation for Splunk's processing language.
* **Core Components**
    * `Core Syntax & Reference Tables.md` - Data types, operators, and reserved keywords.
    * `Discovery: Seeing What Exists.md` - Methods for cataloging indexes and sourcetypes (`tstats`, `metadata`).
* **Pipeline Stages**
    * `Filtering, Searching & Sorting.md` - Search fundamentals.
    * `Field Manipulation.md` - `eval`, `rex`, and field extraction.
    * `Aggregation & Statistics.md` - Grouping and summarizing commands.
    * `Time Series & Metrics.md` - `timechart`, `bin`, and time-based analysis.
    * `Formatting & Visualization.md` - Presentation layer commands.
* **Advanced Implementation**
    * `Advanced Logic & Correlation.md` - Subsearches and complex logic.
    * `How To_Creating Custom Data Structures.md` - Generating inline tables and arrays.
    * `How To_Relationship Analysis (Linking Events).md` - Transaction grouping and joins.
    * `How To_Time Series & Anomaly Detection.md` - Predictive analysis and outlier detection.
    * `How To_Advanced Logic & Filtering.md` - Conditional bucketing and advanced evaluation.

### 2. [Full KQL Reference](./Full%20KQL%20Reference)
Documentation for Azure Data Explorer and Sentinel queries.
* **Core Components**
    * `Core Syntax & Reference Tables.md` - Pipeline structure and variable binding.
* **Pipeline Stages**
    * `Filtering, Searching & Sorting.md` - Predicates and sort operators.
    * `Field Manipulation (The "Transform" Phase).md` - `project`, `extend`, and scalar functions.
    * `Aggregation & Statistics.md` - `summarize` operators and aggregation functions.
    * `Time Series & Metrics.md` - `make-series` and binning.
    * `Formatting & Visualization.md` - `render` operators.
* **Advanced Implementation**
    * `Advanced Logic: Joins, Lookups & Graphs.md` - Multi-table joins and graph semantics (`make-graph`).
    * `How To_Creating Custom Data Structures.md` - `datatable` and dynamic array generation.
    * `How To_Time Series & Anomaly Detection.md` - Native ML and anomaly decomposition.
    * `How To_Advanced Logic & Filtering.md` - Advanced `where` clauses and logic patterns.

### 3. [Full ESQL Reference](./Full%20ESQL%20Reference)
Documentation for Elasticsearch's piped query language.
* **Core Documentation**
    * `Core Syntax & Rules.md` - Source commands (`FROM`) and query structure.
    * `Command Catalog (By Intent).md` - Categorized list of processing commands.
    * `Function Encyclopedia.md` - Reference for scalar, math, and string functions.
* **Advanced Implementation**
    * `Advanced: Anomaly Detection.md` - Implementation of `CHANGE_POINT` for trend analysis.

## Usage
Navigate to the specific language directory to access syntax guides and copy-pasteable examples for data analysis workflows.
