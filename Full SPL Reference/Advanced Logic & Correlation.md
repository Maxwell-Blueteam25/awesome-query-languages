### **VII. Advanced Logic & Correlation**

_Complex operations involving grouping and subsearches._

| Command                | Description                                                                                                                             | Example                                                  |
|------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------|
| `transaction`          | Groups results into "sessions" or "transactions" based on shared fields and time constraints. Adds fields `duration` and `eventcount`. | `transaction host cookie maxspan=30s`                  |
| `lookup`               | Enriches events with fields from an external CSV/KVStore.                                                                               | `lookup user_identities.csv user OUTPUT department`    |
| `inputlookup`          | Loads a lookup table as the primary data source.                                                                                        | `inputlookup known_malware_hashes.csv`                 |
| `outputlookup`         | Writes search results to a lookup file.                                                                                                 | `outputlookup append=t incident_master.csv`            |
| `accum`                | Calculates a running total.                                                                                                             | `accum bytes as total_bytes_transferred`               |
| `delta`                | Computes the difference between current and previous value (useful for beaconing/jitter analysis).                                      | `delta _time as time_gap`                              |
| `trendline`            | Computes moving averages (SMA, EMA, WMA).                                                                                               | `trendline sma5(count) as smooth_traffic`              |
| `anomalydetection`     | Identifies anomalies in a field based on statistical distribution.                                                                      | `anomalydetection method=histogram bytes`             |


#### **Multivalue Field Commands**

_Handling arrays._

|**Command**|**Description**|**Example**|
|---|---|---|
|**`makemv`**|Splits a single string into a multivalued field (array).|`|
|**`nomv`**|Combines an array back into a single string.|`|
|**`mvexpand`**|Creates a new event row for _each_ value in the array.|`|
|**`mvcount(X)`**|Returns the size of the array X.|`|
|**`mvindex(X,Y)`**|Returns the item at index Y in array X.|`|
|**`mvfilter(X)`**|Filters an array based on a boolean expression X.|`mvfilter(match(email, "\.net$"))` |
|**`mvfind(X,Y)`**|Finds the index of a value matching regex Y in array X.|`|


#### **Transaction: Syntax & Eviction Logic**

The `transaction` command is memory-intensive but essential for stitching together multi-stage attacks (e.g., TGT Request -> Service Ticket -> Login).

| Argument / Field        | Purpose                                                                 | DFIR / Hunting Use Case                                                                                 |
|------------------------|-------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| `startswith=<filter>`  | Defines the opening boundary of a transaction.                          | Use `startswith="EventCode=4624"` to begin a session at user logon.                                       |
| `endswith=<filter>`    | Defines the closing boundary of a transaction.                          | Use `endswith="EventCode=4634"` to terminate the session at logoff.                                       |
| `maxspan=<time>`       | Maximum time window a transaction can span from first event.           | Set `maxspan=10h` to prevent long-running or stale sessions from polluting analysis.                     |
| `keepevicted=true`     | Retains evicted / failed transactions instead of discarding them.      | Critical for detecting attack chains that never completed (crashed services, truncated intrusions).      |
| `closed_txn=1`         | Indicates the transaction completed successfully.                      | Confirms the event chain met its defined `endswith` or time boundaries normally.                          |
| `closed_txn=0`         | Indicates the transaction was evicted or never closed properly.        | High-value signal for interrupted attacks, service crashes, or memory-based transaction drops.           |


**Syntax:**

Code snippet

```
| transaction <field_list> [startswith=<filter>] [endswith=<filter>] [maxspan=<time>] [keepevicted=<bool>]
```

**Argument Breakdown:**

- **`startswith=<filter>` / `endswith=<filter>`**:
    
    - Defines the logical boundaries of a transaction.
        
    - **DFIR Use Case:** Use `startswith="EventCode=4624"` (Logon) and `endswith="EventCode=4634"` (Logoff) to encapsulate a full user session.
        
- **`maxspan=<time>`**:
    
    - The maximum length of time a transaction can span (e.g., `10h`). Events falling outside this window relative to the first event are excluded from the group.
        
- **`keepevicted=true`**:
    
    - **Default:** `false` (Splunk discards transactions that violate memory limits or constraints to save resources).
        
    - **True:** Splunk retains "failed" or "evicted" transactions in the results but marks them. This is critical when hunting for events that _started_ but never _finished_ properly (e.g., a crashed service or a truncated attack chain).
        
- **`closed_txn`**:
    
    - A field generated **only** when `keepevicted=true`.
        
    - `closed_txn=1`: The transaction completed successfully (met `endswith` criteria or time limits naturally).
        
    - `closed_txn=0`: The transaction was **evicted**. This usually means it exceeded memory buffers (`maxevents`) or failed to close before the search finalized.
        

