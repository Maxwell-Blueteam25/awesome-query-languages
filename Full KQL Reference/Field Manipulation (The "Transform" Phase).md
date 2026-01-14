### **III. Field Manipulation (The "Transform" Phase)**

_Creating and modifying columns._

#### **1. Selection & Creation**

|**Command**|**Description**|**Example**|
|---|---|---|
|**`project`**|Selects specific columns to keep (renaming allowed).|`project State, EventType`.|
|**`extend`**|**Creates** calculated columns (appends to list).|`extend Duration = EndTime - StartTime`.|
|**`project-away`**|Removes specific columns.|`project-away ColumnName`.|
|**`project-rename`**|Renames columns without dropping others.|`project-rename new_name = old_name`.|
|**`mv-expand`**|Expands multi-value arrays into separate rows.|`mv-expand range`.|
|**`parse`**|Extracts data from strings (like Regex).|`parse kind=regex Expression with ...`.|

#### **2. Scalar Functions (Math & Types)**

|**Function**|**Description**|**Example**|
|---|---|---|
|**`todouble()`**|Converts input to double (crucial for division).|`todouble(Count) / Total`.|
|**`tostring()`**|Converts input to string.|`tostring(features.properties.NAME)`.|
|**`round(X, Y)`**|Rounds X to Y decimal places.|`round(avg(DamageProperty))`.|
|**`isnull()`** / **`isnotnull()`**|Checks for null values.|`where isnotnull(BeginLat)`.|
