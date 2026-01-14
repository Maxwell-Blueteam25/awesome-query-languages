### **IV. Aggregation & Statistics**

_Grouping and calculating. Equivalent to SPL `stats`._

#### **1. Core Aggregation Operator**

**`summarize`** is the primary operator. It groups rows by the `by` clause and calculates the aggregation function.

- **Syntax:** `T | summarize count() by State`.
    

#### **2. Common Aggregation Functions**

_Used inside `summarize`._

|**Function**|**Description**|**Example**|
|---|---|---|
|**`count()`**|Counts rows per group.|`summarize count() by City`.|
|**`countif(P)`**|Counts rows where predicate P is true.|`countif(DamageCrops > 0)`.|
|**`dcount(X)`**|**Distinct** count (approximate).|`dcount(UserID)` (Not explicitly in source, but standard KQL equivalent to `distinct`).|
|**`sum(X)`**|Sum of values.|`sum(DamageCrops)`.|
|**`avg(X)`**|Average of values.|`avg(DamageCrops)`.|
|**`min(X)`** / **`max(X)`**|Minimum / Maximum value.|`max(DamageCrops)`.|
|**`make_set(X)`**|Creates an array of unique values.|`make_set(EventType)`.|
|**`array_length(X)`**|Returns the number of items in an array.|`array_length(StormTypes)`.|
