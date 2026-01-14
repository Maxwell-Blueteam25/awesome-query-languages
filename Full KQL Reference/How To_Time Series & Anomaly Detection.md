### **III. How To: Time Series & Anomaly Detection**

_Security is often about finding the break in the pattern. KQL has built-in ML for this._

#### **1. Handling Missing Data (`make-series`)**

When charting errors over time, if no errors occur at 3:00 PM, a standard `summarize` will skip that hour. `make-series` forces a "0" value for missing bins, creating a consistent timeline.


**Syntax:**

Code snippet

```
make-series ErrorCount = count() default=0 on TimeGenerated step 1h by Computer
```

#### **2. Detecting Anomalies**

Once you have a clean time series (using `make-series`), you can pipe it into `series_decompose_anomalies` to automatically flag spikes or drops.

**Syntax:**

Code snippet

```
| make-series Traffic = avg(Bytes) default=0 on TimeGenerated step 1h by IP
| extend anomalies = series_decompose_anomalies(Traffic)
| render anomalychart with (anomalycolumns=anomalies)
```

#### **3. Sliding Windows**

To calculate a rolling average (e.g., "7-day moving average"), you need more than simple binning.

- **Technique:** Use `bin_at` to align dates, then `range` and `mv-expand` to duplicate rows for the window duration, allowing you to aggregate across overlapping periods.
    
