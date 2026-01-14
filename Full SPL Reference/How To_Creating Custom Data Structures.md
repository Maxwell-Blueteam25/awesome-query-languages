
### **I. Creating Custom Data Structures**

_In Splunk, you often need to generate dummy data for testing or define static lists without creating a permanent CSV file on the backend._

#### **1. How to Make a Table (`makeresults`)**

Unlike KQL's `datatable`, SPL uses a combination of `makeresults` (to create a dummy timestamp) and string manipulation to "fake" a table. This is the standard way to create scratchpad data.

**Syntax (The "Multikv" Method):**

Code snippet

```
| makeresults 
| eval _raw="
Name,RiskScore
UserAdmin,90
ServiceAcct,50
GuestUser,10
" 
| multikv forceheader=1
| table Name, RiskScore
```

_Tip: This forces Splunk to parse the text block as if it were a CSV file._

#### **2. How to Make an Array / List (Multivalue Fields)**

SPL handles arrays as "Multivalue (MV)" fields. You create them using `split` or `makemv`. This is useful for tagging events with multiple categories.

**Syntax:**

Code snippet

```
| eval CriticalServers = split("Server01,DB-PROD,DC-01", ",")
| where host IN ("Server01", "DB-PROD") 
```

_Note: The `IN` operator works best with literal lists. To check against the `CriticalServers` field created above, you would typically use `mvfind`._

#### **3. How to Make a Hashtable / Dictionary**

SPL does not have a native JSON variable type for dictionaries. You have two main options:

- **Option A (Inline Logic):** Use the `case()` function to map keys to values.
    
- **Option B (Lookup File):** The preferred method for management.
    

**Syntax (Inline `case`):**

Code snippet

```
... 
| eval ReadableEvent = case(
    EventID==4624, "Successful Login",
    EventID==4625, "Failed Login",
    EventID==4688, "Process Created",
    true(), "Unknown"
)
```
