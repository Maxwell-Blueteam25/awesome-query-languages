### **III. Function Encyclopedia**

_Used inside `EVAL`, `WHERE`, and `STATS`._

#### **1. Conditional & Logic**

- **`CASE`**: If-Else logic.
    
    - _Example:_ `EVAL status_type = CASE(status >= 500, "Critical", status >= 400, "Error", "OK")`.
        
- **`COALESCE`**: Returns the first non-null value.
    
- **`GREATEST` / `LEAST`**: Returns max/min of a list of values.
    

#### **2. Search Functions**

- **`MATCH`**: Full-text search within a specific field. Supports named parameters for tuning.
    
    - _Syntax:_ `MATCH(message, "error", {"operator": "AND"})`.
        
- **`MATCH_PHRASE`**: Searches for an exact phrase.
    
- **`CIDR_MATCH`**: Checks if an IP falls within a subnet block.
    

#### **3. Date & Time**

- **`NOW()`**: Current time.
    
- **`DATE_TRUNC`**: Rounds time down (floor) to a specific unit.
    
- **`DATE_PARSE`**: Converts string to date.
    
- **`DATE_DIFF`**: Calculates difference between two dates.
    

#### **4. String Manipulation**

- **`CONCAT`**: Joins strings.
    
- **`SPLIT`**: Splits string into an array.
    
- **`TRIM` / `LTRIM` / `RTRIM`**: Removes whitespace.
    
- **`TO_LOWER` / `TO_UPPER`**: Case conversion.
    
- **`RIGHT` / `LEFT` / `SUBSTRING`**: Slicing strings.
    

#### **5. Type Conversion**

- **`TO_STRING`**, **`TO_INTEGER`**, **`TO_DOUBLE`**, **`TO_IP`**, **`TO_BOOLEAN`**.
    
- **`TO_DATETIME`**: Essential for parsing timestamp strings.
    

#### **6. Aggregation Functions (Used in STATS)**

- **Math:** `AVG`, `SUM`, `MIN`, `MAX`, `MEDIAN`, `VAR`, `STD_DEV`.
    
- **Counting:** `COUNT`, `COUNT_DISTINCT`.
    
- **Position:** `TOP` (Top N values), `PERCENTILE`.
    

#### **7. Multivalue (Array) Functions**

- **`MV_COUNT`**: Length of array.
    
- **`MV_CONCAT`**: Joins array into string.
    
- **`MV_DEDUPE`**: Removes duplicates in an array.
    
- **`MV_MIN` / `MV_MAX` / `MV_AVG`**: Stats on array contents.
    
