### **Discovery: Seeing What Exists**

_Before searching for specific logs, you need to know which buckets (indexes) and formats (sourcetypes) are available._

#### **1. How to List All Available Indexes**

You have two main ways to do this. One counts the files on disk (`eventcount`), and the other counts the indexed events (`tstats`).

**Option A: The Disk Check (`eventcount`)** This checks the database storage directly. It is fast but sometimes requires admin permissions.

Code snippet

```
| eventcount summarize=false index=* | table index, count
| sort - count
```

- **Explanation:** `summarize=false` lists every index separately. `index=*` looks at everything (except internal `_` indexes).
    

**Option B: The "Pro" Way (`tstats`)** This uses the high-speed **TSIDX** (Time Series Index) files. It is often faster than searching and works for any user with read access.

Code snippet

```
| tstats count where index=* by index
| sort - count
```

#### **2. How to List All Available Sourcetypes**

Using `metadata` is the fastest way to see "what kind of data" exists without scanning a single raw event.

**Syntax:**

Code snippet

```
| metadata type=sourcetypes index=*
| convert ctime(lastTime)
| table sourcetype, totalCount, lastTime
| sort - totalCount
```

- **Explanation:**
    
    - `metadata`: Queries the database catalog (instant results).
        
    - `lastTime`: Shows you the last time this sourcetype was seen (crucial for checking if a feed is dead).
        
    - `ctime()`: Converts the Unix epoch timestamp into a readable date string.
        

#### **3. How to See Sourcetypes _Per_ Index**

Sometimes you want to know, "What data is inside the `botsv1` index?" The `metadata` command is global, so for specific indexes, use `tstats`.

**Syntax:**

Code snippet

```
| tstats count where index=botsv1 by sourcetype
| sort - count
```

---

### **II. Time & Scope Filtering**

_Defining the boundaries of your search._

#### **1. Selecting Date Ranges (Inline)**

While you usually use the Time Picker UI in Splunk, you can hardcode time ranges using `earliest` and `latest`. This is vital for saved searches or alerts.

**Syntax:**

Code snippet

```
index=botsv1 earliest="08/01/2016:00:00:00" latest="08/31/2016:23:59:59"
```

- **Format:** `MM/DD/YYYY:HH:MM:SS`.
    
- **Relative Time:** You can also use `earliest=-15m` (last 15 minutes) or `earliest=-1d@d` (yesterday start).
    

#### **2. Wildcard Searching**

You don't need to know the exact name of a sourcetype. Use the asterisk `*` to match patterns.

**Syntax:**

Code snippet

```
index=botsv1 sourcetype=fgt* "imreallynotbatman.com"
```

- **Explanation:** This searches the `botsv1` index for any Fortigate firewall logs (`fgt_traffic`, `fgt_utm`, etc.) containing that specific domain.
    

---

