### **I. Core Syntax & Reference Tables**

_The atomic building blocks of a Kusto query._

#### **1. The Pipeline Structure**

KQL uses the pipe (`|`) to pass data from one step to the next.

- **Flow:** Source $\rightarrow$ Filter $\rightarrow$ Summarize $\rightarrow$ Sort $\rightarrow$ Select.
    
- **Comments:** Use `//` to add comments.
    

#### **2. Date & Time Functions**

Used for filtering and bucketing time.

|**Function**|**Description**|**Example**|
|---|---|---|
|**`ago(T)`**|Returns the time offset relative to now.|`ago(1h)` (1 hour ago).|
|**`now()`**|Current time (implied in relative calcs).|`where TimeGenerated > ago(7d)`.|
|**`datetime()`**|specific ISO 8601 date.|`datetime(2007-01-01)`.|
|**`format_datetime(D, F)`**|Formats date D into string format F.|`format_datetime(dt, 'yyyy-MM-dd')`.|
|**`bin(V, R)`**|Rounds values (usually time) to a bucket size R.|`bin(StartTime, 7d)`.|

#### **3. Common Operators & Logic**

|**Operator**|**Description**|**Syntax / Example**|
|---|---|---|
|**`let`**|Binds a name to a value or expression (Variable).|`let windowStart = datetime(2007-07-01);`.|
|**`case`**|Conditional logic (If-ElseIf-Else).|`case(Injuries > 50, "Large", Injuries > 0, "Small", "None")`.|
|**`iff`**|Simple If/Else.|`iff(bin > windowEnd, windowEnd, bin)`.|
