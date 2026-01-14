### **III.How To: Time Series & Anomaly Detection**

_Splunk excels at time-series analysis with powerful stats commands._

#### **1. Handling Missing Data (`makecontinuous`)**

If you `timechart` errors and there are zero errors at 3:00 PM, Splunk might leave a gap. Use `fillnull` or `makecontinuous` to ensure the line chart doesn't break.

**Syntax:**

Code snippet

```
... 
| timechart span=1h count by host 
| fillnull value=0
```

_Note: `timechart` often does this automatically, but `makecontinuous` enforces a timeline on raw data before aggregation._

#### **2. Detecting Anomalies (`predict` & `anomalydetection`)**

Splunk can forecast future values or flag outliers without complex ML Toolkit setups.

Syntax (Predict):

Draws a trendline and a future forecast interval.

Code snippet

```
... | timechart span=1h count 
| predict count future_timespan=24
```

Syntax (Outliers):

Automatically filters for events that are statistically unexpected.

Code snippet

```
... | anomalydetection method=histogram action=filter
```
