
# **Flight Data 2024 - Complete Data Dictionary**

## **Dataset Overview**
- **Source:** BTS TranStats On-Time Performance Database
- **Period:** January - December 2024
- **Total Records:** ~7 Million
- **Columns:** 35
- **Format:** CSV
- **License:** CC0 (Public Domain)

**Dataset Link:** [Flight Data 2024 on Kaggle](https://www.kaggle.com/datasets/hrishitpatil/flight-data-2024)

---

## **Complete Column Reference**

### **1. Flight Identification & Timing**

| Column | Data Type | Null % | Description | Example |
|--------|-----------|--------|-------------|---------|
| `year` | Int64 | 0.0% | Year of the flight | `2024` |
| `month` | Int64 | 0.0% | Month (1-12) | `1` |
| `day_of_month` | Int64 | 0.0% | Day of the month (1-31) | `1` |
| `day_of_week` | Int64 | 0.0% | Day of week (1=Monday, 7=Sunday) | `1` |
| `fl_date` | datetime64[ns] | 0.0% | Flight date (YYYY-MM-DD) | `2024-01-01` |

### **2. Carrier & Flight Info**

| Column | Data Type | Null % | Description | Example |
|--------|-----------|--------|-------------|---------|
| `op_unique_carrier` | object | 0.0% | Unique carrier code (airline) | `"AA"` |
| `op_carrier_fl_num` | float64 | 0.0% | Flight number for reporting airline | `148.0` |

### **3. Origin Airport**

| Column | Data Type | Null % | Description | Example |
|--------|-----------|--------|-------------|---------|
| `origin` | object | 0.0% | Origin airport IATA code | `"JFK"` |
| `origin_city_name` | object | 0.0% | Origin city and state | `"New York, NY"` |
| `origin_state_nm` | object | 0.0% | Origin state name | `"New York"` |

### **4. Destination Airport**

| Column | Data Type | Null % | Description | Example |
|--------|-----------|--------|-------------|---------|
| `dest` | object | 0.0% | Destination airport IATA code | `"LAX"` |
| `dest_city_name` | object | 0.0% | Destination city and state | `"Los Angeles, CA"` |
| `dest_state_nm` | object | 0.0% | Destination state name | `"California"` |

### **5. Departure Times & Delays**

| Column | Data Type | Null % | Description | Example |
|--------|-----------|--------|-------------|---------|
| `crs_dep_time` | Int64 | 0.0% | Scheduled departure time (HHMM, local) | `1252` |
| `dep_time` | float64 | 1.31% | Actual departure time (HHMM, local) | `1247.0` |
| `dep_delay` | float64 | 1.31% | Departure delay in minutes (negative if early) | `-5.0` |
| `taxi_out` | float64 | 1.35% | Taxi-out time in minutes | `31.0` |
| `wheels_off` | float64 | 1.35% | Wheels-off time (HHMM, local) | `1318.0` |

### **6. Arrival Times & Delays**

| Column | Data Type | Null % | Description | Example |
|--------|-----------|--------|-------------|---------|
| `wheels_on` | float64 | 1.38% | Wheels-on time (HHMM, local) | `1442.0` |
| `taxi_in` | float64 | 1.38% | Taxi-in time in minutes | `7.0` |
| `crs_arr_time` | Int64 | 0.0% | Scheduled arrival time (HHMM, local) | `1508` |
| `arr_time` | float64 | 1.38% | Actual arrival time (HHMM, local) | `1449.0` |
| `arr_delay` | float64 | 1.61% | Arrival delay in minutes (negative if early) | `-19.0` |

### **7. Flight Status**

| Column | Data Type | Null % | Description | Example |
|--------|-----------|--------|-------------|---------|
| `cancelled` | int64 | 0.0% | Cancellation indicator (0=No, 1=Yes) | `0` |
| `cancellation_code` | object | 98.64% | Reason for cancellation (A=Carrier, B=Weather, C=NAS, D=Security) | `"B"` |
| `diverted` | int64 | 0.0% | Diversion indicator (0=No, 1=Yes) | `0` |

### **8. Flight Duration & Distance**

| Column | Data Type | Null % | Description | Example |
|--------|-----------|--------|-------------|---------|
| `crs_elapsed_time` | float64 | 0.0% | Scheduled elapsed time in minutes | `136.0` |
| `actual_elapsed_time` | float64 | 1.61% | Actual elapsed time in minutes | `122.0` |
| `air_time` | float64 | 1.61% | Flight time in minutes (wheels-off to wheels-on) | `84.0` |
| `distance` | float64 | 0.0% | Distance between airports in miles | `509.0` |

### **9. Delay Root Causes**

| Column | Data Type | Null % | Description | Example |
|--------|-----------|--------|-------------|---------|
| `carrier_delay` | int64 | 0.0% | Carrier-related delay in minutes | `0` |
| `weather_delay` | int64 | 0.0% | Weather-related delay in minutes | `0` |
| `nas_delay` | int64 | 0.0% | National Air System delay in minutes | `0` |
| `security_delay` | int64 | 0.0% | Security delay in minutes | `0` |
| `late_aircraft_delay` | int64 | 0.0% | Late aircraft delay in minutes | `0` |

---

## **Sample Data Preview**

| year | month | day_of_month | day_of_week | fl_date | op_unique_carrier | op_carrier_fl_num | origin | origin_city_name | origin_state_nm | dest | dest_city_name | dest_state_nm | crs_dep_time | dep_time | dep_delay | taxi_out | wheels_off | wheels_on | taxi_in | crs_arr_time | arr_time | arr_delay | cancelled | cancellation_code | diverted | crs_elapsed_time | actual_elapsed_time | air_time | distance | carrier_delay | weather_delay | nas_delay | security_delay | late_aircraft_delay |
|------|-------|--------------|-------------|---------|-------------------|-------------------|--------|------------------|-----------------|------|-----------------|---------------|---------------|----------|-----------|----------|------------|-----------|---------|---------------|----------|-----------|-----------|-------------------|----------|------------------|---------------------|----------|----------|---------------|---------------|-----------|----------------|---------------------|
| 2024 | 4 | 18 | 4 | 2024-04-18 | MQ | 3535.0 | DFW | Dallas/Fort Worth, TX | Texas | RAP | Rapid City, SD | South Dakota | 1018 | 1015.0 | -3.0 | 21.0 | 1036.0 | 1135.0 | 4.0 | 1149 | 1139.0 | -10.0 | 0 | | 0 | 151.0 | 144.0 | 119.0 | 835.0 | 0 | 0 | 0 | 0 | 0 |
| 2024 | 1 | 1 | 1 | 2024-01-01 | AA | 148.0 | CLT | Charlotte, NC | North Carolina | PHX | Phoenix, AZ | Arizona | 1637 | 1633.0 | -4.0 | 14.0 | 1647.0 | 1900.0 | 6.0 | 1923 | 1906.0 | -17.0 | 0 | | 0 | 286.0 | 273.0 | 253.0 | 1773.0 | 0 | 0 | 0 | 0 | 0 |
| 2024 | 12 | 12 | 4 | 2024-12-12 | 9E | 5440.0 | CHA | Chattanooga, TN | Tennessee | ATL | Atlanta, GA | Georgia | 1000 | 952.0 | -8.0 | 13.0 | 1005.0 | 1034.0 | 8.0 | 1059 | 1042.0 | -17.0 | 0 | | 0 | 59.0 | 50.0 | 29.0 | 106.0 | 0 | 0 | 0 | 0 | 0 |

---

## **Data Quality Notes**

### **Missing Values Strategy:**
- **Delay columns** (`carrier_delay`, `weather_delay`, `nas_delay`, `security_delay`, `late_aircraft_delay`): Missing values filled with `0`
- **Time columns** (`dep_time`, `arr_time`, etc.): Preserved as original, null percentages as shown above
- **Cancellation codes**: High null percentage (98.64%) as only present for cancelled flights

### **Data Cleaning Applied:**
1. **Column standardization**: Converted to snake_case naming convention
2. **Date formatting**: `fl_date` standardized to ISO format (YYYY-MM-DD)
3. **Binary indicators**: `cancelled` and `diverted` converted to 0/1
4. **Merging**: Monthly files (Jan-Dec 2024) combined into single dataset
5. **Missing values**: Delay columns filled with 0 where null

---

## **Key Data Relationships**

### **Primary Key:**
- Composite key: `fl_date` + `op_unique_carrier` + `op_carrier_fl_num` + `origin` + `dest`

### **Time Calculations:**
- **Actual elapsed time** = `actual_elapsed_time` (minutes)
- **Scheduled elapsed time** = `crs_elapsed_time` (minutes)
- **Air time** = `air_time` (minutes)
- **Taxi time** = `taxi_out` + `taxi_in` (minutes)

### **Delay Relationships:**
```
total_delay = carrier_delay + weather_delay + nas_delay + security_delay + late_aircraft_delay
arr_delay ≈ dep_delay + (actual_elapsed_time - crs_elapsed_time)
```

---

## **Usage Examples**

### **SQL Query Examples:**
```sql
-- Get delayed flights
SELECT * FROM flight_data 
WHERE arr_delay > 15 
  AND cancelled = 0 
  AND diverted = 0;

-- Calculate airline on-time performance
SELECT op_unique_carrier,
       COUNT(*) as total_flights,
       AVG(arr_delay) as avg_delay,
       SUM(CASE WHEN arr_delay <= 15 THEN 1 ELSE 0 END) * 100.0 / COUNT(*) as on_time_percentage
FROM flight_data 
WHERE cancelled = 0 
GROUP BY op_unique_carrier 
ORDER BY on_time_percentage DESC;

-- Find busiest routes
SELECT origin, dest, 
       COUNT(*) as flight_count,
       AVG(arr_delay) as avg_delay
FROM flight_data 
WHERE cancelled = 0 
GROUP BY origin, dest 
ORDER BY flight_count DESC 
LIMIT 10;
```

### **Python/Pandas Examples:**
```python
import pandas as pd

# Load data
df = pd.read_csv('flight_data_2024.csv')

# Calculate basic statistics
delayed_flights = df[df['arr_delay'] > 15].shape[0]
total_flights = df.shape[0]
delay_percentage = (delayed_flights / total_flights) * 100

# Group by airline
airline_stats = df.groupby('op_unique_carrier').agg({
    'arr_delay': 'mean',
    'cancelled': 'sum',
    'flight_id': 'count'
}).rename(columns={'flight_id': 'total_flights'})
```

---

## **File Structure in Dataset**

```
Flight Data 2024/
├── flight_data_2024.csv           # Full dataset (~7M rows)
├── flight_data_2024_sample.csv    # Sample (10,000 rows)
├── flight_data_2024_data_dictionary.csv  # This dictionary
├── README.md                      # Dataset overview
├── LICENSE.txt                    # CC0 License
└── dataset-metadata.json          # Kaggle metadata
```

---

## **Citation**

If you use this dataset in your research or projects, please cite:

```bibtex
@dataset{flight_data_2024,
  author = {BTS TranStats and Hrishit Patil},
  title = {Flight Delay Dataset 2024},
  year = {2024},
  publisher = {Kaggle},
  url = {https://www.kaggle.com/datasets/hrishitpatil/flight-data-2024}
}
```

---

## **License**

This dataset is released under **CC0 1.0 Universal (CC0 1.0) Public Domain Dedication**. You can copy, modify, distribute and perform the work, even for commercial purposes, all without asking permission.

---

**Last Updated:** November 2024  
**Maintainer:** Abdelrhman Anwar (abd.ahm.anwar@gmail.com)

---
