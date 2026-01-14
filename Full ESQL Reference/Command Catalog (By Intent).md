### **II. Command Catalog (By Intent)**

#### **1. The "Source" Phase (Start Here)**

You cannot pipe _into_ nothing; you must pull data first.

- **`FROM`**: The primary starting point. Pulls data from an index.
    
    - _Usage:_ `FROM my-index-*`
        
- **`ROW`**: Generates a static row (useful for testing logic without an index).
    
    - _Usage:_ `ROW key=[1, 2, 3]`
        

#### **2. Filtering & Searching (The "Where" Phase)**

- **`WHERE`**: Filters rows based on boolean logic.
    
    - _Usage:_ `| WHERE response_code >= 400`
        
- **`LIMIT`**: Keeps only the first N rows (equivalent to SPL `head`).
    
    - _Usage:_ `| LIMIT 5`
        
- **`DROP`**: Removes specific columns (fields) from the output.
    
    - _Usage:_ `| DROP internal_id`
        
- **`KEEP`**: The inverse of DROP; keeps _only_ specified columns (equivalent to SPL `fields`).
    
    - _Usage:_ `| KEEP @timestamp, message`
        
- **`SAMPLE`**: Reduces dataset size by sampling.
    

#### **3. Processing & Transformation (The "Eval" Phase)**

- **`EVAL`**: Creates or updates columns with calculated values (Math, String, Date functions).
    
    - _Usage:_ `| EVAL duration_sec = duration_ms / 1000`
        
- **`RENAME`**: Renames a column.
    
    - _Usage:_ `| RENAME src_ip AS SourceIP`
        
- **`DISSECT`**: Extracts fields using a fixed delimiter pattern (fast, strict).
    
- **`GROK`**: Extracts fields using Regex patterns (flexible, slower).
    
- **`MV_EXPAND`**: Explodes a multi-value array into separate rows (equivalent to SPL `mvexpand`).
    
    - _Usage:_ `| MV_EXPAND tags`.
        
- **`SORT`**: Orders the results.
    
    - _Usage:_ `| SORT @timestamp DESC`
        

#### **4. Aggregation & Grouping (The "Stats" Phase)**

- **`STATS`**: The core aggregation command.
    
    - _Usage:_ `| STATS count = COUNT(id) BY host`.
        
- **`BUCKET`**: Groups data into buckets (often used with time).
    
    - _Usage:_ Used inside `STATS` or grouping contexts.
        

#### **5. Advanced Logic & Machine Learning**

- **`ENRICH`**: Adds data from an enrichment policy (similar to lookups).
    
- **`LOOKUP JOIN`**: Joins against a lookup index.
    
- **`CHANGE_POINT`**: Detects anomalies (spikes, dips, trend changes) in a time series.
    
    - _Syntax:_ `CHANGE_POINT value_col ON timestamp_col`
        
    - _Output:_ Adds `type` (spike, dip, step_change) and `pvalue` columns.
        
