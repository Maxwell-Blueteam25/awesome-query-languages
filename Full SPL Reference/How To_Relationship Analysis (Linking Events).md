### **IV. Relationship Analysis (Linking Events)**

_Correlating disparate events into a single story._

#### **1. Grouping by ID (`transaction`)**

This groups separate events (e.g., a "Login", "File Access", and "Logout") into a single "session" block based on a shared ID or time proximity.

**Syntax:**

Code snippet

```
... | transaction SessionID maxspan=30m startsWith="Login" endsWith="Logout"
```

_Result: Produces one row per session containing all the raw text from the grouped events._

#### **2. Joining Data (`join`)**

Similar to SQL, merging two datasets on a specific field.

Warning: join in Splunk is resource-intensive. Use stats or lookup if possible.

**Syntax:**

Code snippet

```
index=main 
| join type=left host [ search index=asset_inventory | fields host, owner, location ]
```

