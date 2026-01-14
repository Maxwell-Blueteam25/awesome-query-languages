### **IV. Advanced: Anomaly Detection**

ES|QL includes native time-series analysis commands that require a Platinum license.

**Scenario:** Detect a sudden "Step Change" (e.g., a deployment caused CPU to jump from 20% to 60% and stay there).

**Syntax:**

SQL

```
FROM metrics-index
| STATS avg_cpu = AVG(cpu.usage) BY @timestamp
| CHANGE_POINT avg_cpu ON @timestamp
| WHERE type == "step_change"
```

**Output Types:**

- `spike`: Short-lived increase.
    
- `dip`: Short-lived decrease.
    
- `step_change`: Sustained shift in value distribution.
    
- `trend_change`: Change in the slope of the trend.
    
