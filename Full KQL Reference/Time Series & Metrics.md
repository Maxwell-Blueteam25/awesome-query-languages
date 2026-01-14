### **V. Time Series & Metrics**

_Handling data over time._

|**Command**|**Description**|**Example**|
|---|---|---|
|**`make-series`**|Creates a complete time series (fills gaps with default).|`make-series avg(Damage) default=0 on StartTime step 7d`.|
|**`bin`**|Used inside `summarize` to bucket time.|`summarize count() by bin(StartTime, 7d)`.|
|**`series_decompose_anomalies`**|Finds anomalies in a series.|`extend anomalies = series_decompose_anomalies(damage)`.|
