### **I. How To: Creating Custom Data Structures**

_Sometimes you need to create data from scratch to act as a whitelist, blacklist, or lookup table without importing an external CSV._

#### **1. How to Make a Table (`datatable`)**

Use `datatable` to define a temporary table manually within your query. This is perfect for creating a static list of known bad IPs or users to join against your live data1111.

+1

**Syntax:**

Code snippet

```
let BadActors = datatable(Name:string, RiskScore:int)
[
    "UserAdmin", 90,
    "ServiceAcct", 50,
    "GuestUser", 10
];
BadActors
```

#### **2. How to Make an Array / List (`dynamic`)**

Use the `dynamic()` keyword with square brackets `[]` to create an array. This is essential for defining lists of items to check against using the `in` operator2.

**Syntax:**

Code snippet

```
let CriticalServers = dynamic(["Server01", "DB-PROD", "DC-01"]);
SecurityEvent
| where Computer in (CriticalServers)
```

Note: You can also generate arrays from existing data using `make_set()`3333.

+1

#### **3. How to Make a Hashtable / Dictionary**

Use `dynamic()` with JSON-like curly braces `{}` to create key-value pairs. This allows you to map obscure codes to human-readable names (e.g., EventIDs to Descriptions) 4.

**Syntax:**

Code snippet

```
let EventMapping = dynamic({
    "4624": "Successful Login",
    "4625": "Failed Login",
    "4688": "Process Created"
});
SecurityEvent
| extend ReadableEvent = EventMapping[tostring(EventID)]
```

---
