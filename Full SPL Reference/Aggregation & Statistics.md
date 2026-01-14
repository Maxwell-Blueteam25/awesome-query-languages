### **IV. Aggregation & Statistics**

_The "Summarize" phase: Counting and calculating._

#### **1. Core Aggregation Commands**

|**Command**|**Description**|**Syntax / Example**|
|---|---|---|
|**`stats`**|Provides statistics, grouped optionally by fields.|`|
|**`eventstats`**|Computes stats and adds them inline to original events.|`|
|**`streamstats`**|Rolling aggregation (cumulative).|`|
|**`top`** / **`rare`**|Displays most/least common values.|`|

#### **2. Common Stats Functions**

_Used inside `stats`, `timechart`, `chart`._

|**Function**|**Description**|
|---|---|
|**`count(X)`**|Count occurrences. Use `eval` for logic: `count(eval(status=500))`.|
|**`dc(X)`**|Distinct Count (count of unique values).|
|**`sum(X)`**|Sum of values.|
|**`avg(X)`**|Average of values.|
|**`max(X)`** / **`min(X)`**|Maximum / Minimum value.|
|**`median(X)`**|Middle-most value.|
|**`mode(X)`**|Most frequent value.|
|**`stdev(X)`**|Sample standard deviation.|
|**`perc<X>(Y)`**|X-th percentile of field Y. E.g., `perc95(total)`.|
|**`values(X)`**|Returns a list of distinct values (alphabetical order).|
|**`list(X)`**|Returns a list of all values (order of appearance).|
|**`earliest(X)`**|Chronologically earliest seen value.|
