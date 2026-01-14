### **II. How To: Advanced Logic & Filtering**

_Techniques to handle complex conditions efficiently._

#### **1. Using Arrays for "In" Logic**

Instead of writing `where x == "a" or x == "b" or x == "c"`, define a list and check against it.

- **Usage:** Use the `in` operator to check if a value exists within your defined array/list.
    
    +2
    
- **Example:** `where EventType in ("Tornado", "Flood", "Wildfire")`.
    

#### **2. Static Mapping (Enrichment)**

Use the hashtable method mentioned above to replace values in your results without a heavy `join`.

- **Scenario:** Mapping "Emergency Manager" to "Public" and "Utility Company" to "Private" .
    
- **Example:** `project FriendlyName = sourceMapping[Source]`.
    

#### **3. Conditional Bucketing (`case`)**

Instead of multiple `where` statements, use `case()` to create categories based on logic (e.g., Risk Levels).

+1

**Syntax:**

Code snippet

```
| extend RiskLevel = case(
    Injuries > 50, "Critical",
    Injuries > 10, "High",
    Injuries > 0,  "Medium",
    "Low"
)
```

This evaluates conditions in order; the first one that matches is returned.
