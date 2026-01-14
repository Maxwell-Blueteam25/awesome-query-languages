### **VII. Advanced Logic: Joins, Lookups & Graphs**

_Combining datasets and complex relationships._

#### **1. Joins & Lookups**

|**Command**|**Description**|**Syntax / Example**|
|---|---|---|
|**`join`**|Merges two tables. Supports `inner`, `leftouter`, etc.|`|
|**`lookup`**|Enriches a fact table with a dimension table (optimized).|`|
|**`union`**|Appends rows from multiple tables.|`union Table1, Table2`.|

#### **2. Graph Semantics**

Modeling interconnected data (Nodes & Edges).

|**Command**|**Description**|**Example**|
|---|---|---|
|**`make-graph`**|Creates a graph from edges and nodes.|`make-graph employee --> manager with employees on name`.|
|**`graph-match`**|Matches patterns in the graph.|`graph-match (alice) <-[reports]-(employee)`.|

#### **3. Geospatial Functions**

| **Function**                     | **Description**                      | **Example**                                           |
| -------------------------------- | ------------------------------------ | ----------------------------------------------------- |
| **`geo_point_in_polygon`**       | Checks if a point is inside a shape. | `geo_point_in_polygon(Lon, Lat, polygon)`.          |
| **`geo_distance_point_to_line`** | Calculates distance to a line.       | `geo_distance_point_to_line(Lon, Lat, line) < 500`. |
