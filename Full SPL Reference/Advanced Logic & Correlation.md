### **VII. Advanced Logic & Correlation**

_Complex operations involving grouping and subsearches._

|**Command**|**Description**|**Example**|
|---|---|---|
|**`transaction`**|Groups results into transactions based on time/fields.|`|
|**`lookup`**|Enriches events with fields from an external CSV/KVStore.|`|
|**`inputlookup`**|Loads a lookup table as the primary data source.|`|
|**`outputlookup`**|Writes search results to a lookup file.|`|
|**`accum`**|Calculates a running total.|`|
|**`delta`**|Computes the difference between current and previous value.|`|
|**`trendline`**|Computes moving averages (SMA, EMA, WMA).|`|
|**`anomalydetection`**|Identifies anomalies in a field.|`|

#### **Multivalue Field Commands**

_Handling arrays._

|**Command**|**Description**|**Example**|
|---|---|---|
|**`makemv`**|Splits a single string into a multivalued field (array).|`|
|**`nomv`**|Combines an array back into a single string.|`|
|**`mvexpand`**|Creates a new event row for _each_ value in the array.|`|
|**`mvcount(X)`**|Returns the size of the array X.|`|
|**`mvindex(X,Y)`**|Returns the item at index Y in array X.|`|
|**`mvfilter(X)`**|Filters an array based on a boolean expression X102.|`mvfilter(match(email, "\.net$"))` |
|**`mvfind(X,Y)`**|Finds the index of a value matching regex Y in array X.|`|
