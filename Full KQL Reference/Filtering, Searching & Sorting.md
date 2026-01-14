### **II. Filtering, Searching & Sorting**

_The "Input" phase: Getting the right events._

|**Command**|**Description**|**Syntax / Example**|
|---|---|---|
|**`where`**|Filters rows on a specific predicate.|`where State == 'TEXAS'`.|
|**`search`**|Text search across **all** columns (slower).|`search "error"` or `search kind=case_insensitive "Error"`.|
|**`take` / `limit`**|Returns a random sample of N rows.|`take 5`.|
|**`top`**|Returns the first N rows _sorted_ by a column.|`top 5 by DamageProperty`.|
|**`sort`**|Sorts the rows (default descending).|`sort by Count desc`.|
|**`distinct`**|Returns unique combinations of columns.|`distinct EventType`.|
|**`between`**|Filters for a range of values (inclusive).|`where StartTime between (datetime(2007-08-01)..datetime(2007-08-30))`.|
