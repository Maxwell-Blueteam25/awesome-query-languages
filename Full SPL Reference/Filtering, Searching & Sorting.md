### **II. Filtering, Searching & Sorting**

_The "Input" phase: Getting the right events from disk._

|**Command**|**Description**|**Syntax / Example**|
|---|---|---|
|**`search`**|Filters results to those that match an expression. Implied at the start of a pipeline16.|`index=main error NOT debug`|
|**`where`**|Filters results using `eval` expressions. Used to compare two different fields17.|`|
|**`dedup`**|Removes subsequent results that match a specified criterion18.|`|
|**`head`**|Returns the first N results19.|`|
|**`tail`**|Returns the last N results20.|`|
|**`sort`**|Sorts search results by specified fields21.|`|
|**`reverse`**|Reverses the order of a result set22.|`|
