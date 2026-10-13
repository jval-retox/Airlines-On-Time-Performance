# Airline On-Time Performance Data Analysis

**Author:** Jiri Valenta

## Overview

This Jupyter notebook analyzes the **"Airline On-Time Performance Data"** dataset covering flights in the United States from 1987 to 2008. The dataset includes information about carriers, arrival and departure delays, cancellation reasons, and other flight metrics collected by the Office of Airline Information, Bureau of Transportation Statistics (BTS).

The notebook uses exploratory data visualization techniques to analyze patterns, trends, and relationships in airline performance metrics over this 21-year period.

## Table of Contents

1. [Preliminary Wrangling](#preliminary-wrangling)
2. [Univariate Exploration](#univariate-exploration)
3. [Bivariate Exploration](#bivariate-exploration)
4. [Multivariate Exploration](#multivariate-exploration)
5. [Conclusions](#conclusions)

---

## Preliminary Wrangling

### Data Source

The original dataset is extensive—uncompressed, it spans 12GB across 22 CSV files organized by year. Due to processing constraints, samples of 10,000 rows from each year's file were extracted and merged into a consolidated ~25MB CSV file. This sampled dataset is used to demonstrate data visualization techniques.

### Data Preparation Steps

1. **Date Parsing**: Year, month, and day columns are parsed into a `Date` column of type Timestamp
2. **Categorical Conversion**: 
   - `CancellationCode` converted to descriptive categorical values (Carrier, Weather, NAS, Security)
   - `DayOfWeek` converted to ordered categorical values (Mon-Sun)
3. **Data Cleaning**:
   - Removed or recoded invalid values (negative airtimes, outlier taxi times)
   - Dropped `TailNum` column due to extensive missing data
   - Converted time values to proper timestamp format
4. **Feature Engineering**:
   - Created `DepTS` column combining `Date` and `DepTime` for complete departure timestamps
   - Converted delay and elapsed time columns to integers
5. **Data Export**: Cleaned dataframe saved as `sample_flights_2009_clean.csv`

### Dataset Characteristics

- **Structure**: Single table with rows representing individual flights
- **Time Period**: 1987-2008 (21 years of data)
- **Total Records**: 220,000 flights
- **Columns**: 27 features including delays, times, carriers, airports, and cancellation reasons
- **Key Metrics**: Departure delay, arrival delay, airtime, distance, taxi-in/out times, delay codes

### Features of Interest

- **Primary Focus**: Departure and arrival delays and temporal trends
- **Secondary Analysis**: Carrier performance, cancellation patterns
- **Supporting Features**: 
  - `DepTS` for timeseries analysis
  - `UniqueCarrier` for carrier identification
  - Airport codes and cancellation reason codes

---

## Univariate Exploration

This section analyzes the distribution of individual variables using histograms and bar charts.

### Question 1: What is the overall distribution of departure and arrival delays?

- Departure delays show a narrower, right-skewed distribution
- Arrival delays have higher deviation due to accumulated delays during flight
- Notable finding: Many flights depart/arrive earlier than scheduled

### Question 2: What is the typical airtime distribution?

- Most flights cluster around 40 minutes airtime
- Dataset contains predominantly short-haul domestic flights

### Question 3: Distance distribution

- Distribution mirrors airtime patterns as expected
- Maximum distance: Honolulu (HNL) to Newark (NJ) route

### Question 4: Departure patterns by day of week

- **Findings**: Saturday and Sunday are the least busy days
- Weekdays show significantly higher flight volumes

### Question 5: Busiest departure hours

- Main operations begin after 6 AM
- Peak departure hours: 8 AM, 1 PM, and 5 PM
- Minimal night operations due to airport regulations

### Question 6: Airports with highest departure delays

- High delays concentrated at smaller regional airports
- SPN (Saipan International) and FCA (Glacier Park) show highest averages
- Note: Small sample sizes make these less representative

### Question 7: Monthly cancellation vulnerability

**Key Finding**: Unusual peak in September cancellations

- Expected pattern: Higher winter month cancellations (northern hemisphere)
- September 2001: ~22% monthly average driven by 9/11 attacks
- Daily data shows near 100% cancellation rates immediately after 9/11

### Question 8: Yearly delay trends

- **Notable years**: 
  - 1996: Olympics in Atlanta causing disruptions
  - 2000: Y2K bubble impact
  - 2001-2002: 9/11 aftermath (followed by delay reduction)
  - 2007-2008: Global Financial Crisis impact
- Pattern: Economic disruptions reduce flights, lowering congestion and delays

### Question 9: Airline performance

- **Best Performer**: Hawaiian Airlines (HA) only carrier with average early departures
- Result prompted deeper investigation into HA's operational excellence

---

## Bivariate Exploration

This section investigates relationships between pairs of variables.

### Variable Correlations

- **Strong correlations**: Distance ↔ Airtime (as expected)
- **Weak correlations**: Most other variable pairs
- **Exception**: Departure delay ↔ Arrival delay (strong positive correlation)

### Question 10: Relationship between departure and arrival delays

**Findings**:
- Strong positive correlation between departure and arrival delays
- Most flights cluster near "on-time" area
- Significant proportion of flights depart late but arrive on-time
- Suggests airlines make up delays during flight by flying faster

### Question 11: Delay code proportions and trends (2003-2008)

**Visual patterns**:
- **Weather delays**: Trending downward (improved weather prediction/management)
- **Late aircraft delays**: Trending upward (increased complexity from connecting flights)
- **Security delays**: Minimal impact (few occurrences)

**Interpretation**: 
- Technology improvements help manage weather
- Increased air traffic complexity causes cascading delays from late connections

### Question 12: Route-based delay patterns

**Key observation**: Horizontal and vertical line patterns in origin-destination heatmap

- Delays predominantly airport-related (not route-specific)
- Atlanta (ATL) exhibits consistently high delays whether origin or destination
- Suggests airport infrastructure/operations affect delay performance

### Question 13: Average delays by reason

**Violin plot analysis**:
- Weather and late aircraft delays: Longer duration when they occur
- Other delay types: Shorter typical durations
- Note: Plot shows distribution shape, not proportional frequency

---

## Multivariate Exploration

This section explores relationships among multiple variables simultaneously.

### Question 14: Departure/arrival delays across carriers

**Distribution findings**:
- Boxplots show carrier-specific delay patterns
- Hawaiian (HA) stands out with consistently early departures/arrivals
- Arrival delays show wider spread than departure delays (accumulated delays)

### Question 15: Departure/arrival delays vs. airtime

**Key discovery**: Lower-right quadrant (late departure, early arrival)

- Flights in this region tend to be longer-haul (darker coloring in visualization)
- Longer flights have more time to make up departure delays
- Airlines utilize faster flying speeds on longer routes to recover time

### Hawaiian Airlines Deep Dive

**Background**: HA showed exceptional on-time performance in initial analysis

**Historical data**:
- Before 2004: High variability in on-time performance
- Since 2004: Consistent early departures/arrivals
- Significant improvement starting in 2004

**Analysis**: Honolulu (HNL) hub vs. other airports

- No significant difference between HNL and other airports
- Early departures not limited to home airport
- Demonstrates system-wide operational excellence at HA

---

## Conclusions

### Key Findings

1. **Data Quality**: Successfully cleaned and prepared 220,000 flight records with minimal data loss
2. **Delay Patterns**: Strong correlation between departure and arrival delays; airlines recover some delays mid-flight
3. **Temporal Trends**: Economic disruptions (Y2K, 9/11, GFC) temporarily reduced delays through lower traffic volume
4. **Carrier Performance**: Hawaiian Airlines achieves industry-leading on-time performance across all operations
5. **Airport Effects**: Delays are predominantly airport-related; specific airports consistently underperform
6. **Cancellations**: 9/11 created unprecedented disruption; weather and carrier reasons typically cited

### Methodology

- Used exploratory data visualization techniques throughout
- Employed multiple visualization types: histograms, scatter plots, heatmaps, boxplots, violin plots
- Combined univariate, bivariate, and multivariate analyses for comprehensive understanding
- Filtered outliers where appropriate for clearer pattern visualization

### Data Files Generated

- `sample_flights_2009.csv` - Initial merged sample
- `sample_flights_2009_clean.csv` - Cleaned and processed dataset

---

## Dataset Dictionary

| Column | Type | Description |
|--------|------|-------------|
| Date | datetime | Flight departure date |
| DayOfWeek | category | Day of week (Mon-Sun) |
| DepTime | datetime | Actual departure time |
| ArrTime | datetime | Actual arrival time |
| CRSDepTime | datetime | Scheduled departure time |
| CRSArrTime | datetime | Scheduled arrival time |
| UniqueCarrier | object | Airline carrier code |
| FlightNum | int | Flight number |
| ActualElapsedTime | int | Actual flight duration (minutes) |
| CRSElapsedTime | int | Scheduled flight duration (minutes) |
| AirTime | int | Time in air (minutes) |
| ArrDelay | int | Arrival delay (minutes) |
| DepDelay | int | Departure delay (minutes) |
| Origin | object | Departure airport code |
| Dest | object | Destination airport code |
| Distance | float | Distance between airports (miles) |
| TaxiIn | int | Taxi-in time (minutes) |
| TaxiOut | int | Taxi-out time (minutes) |
| Cancelled | int | Cancellation indicator (0/1) |
| CancellationCode | category | Reason for cancellation |
| Diverted | int | Diversion indicator (0/1) |
| CarrierDelay | int | Delay due to carrier (minutes) |
| WeatherDelay | int | Delay due to weather (minutes) |
| NASDelay | int | Delay due to NAS (minutes) |
| SecurityDelay | int | Delay due to security (minutes) |
| LateAircraftDelay | int | Delay due to late aircraft (minutes) |
| DepTS | datetime | Full departure timestamp |

---

**Note**: This analysis demonstrates exploratory data visualization techniques applied to real-world aviation performance data. Findings support evidence-based understanding of airline operations, infrastructure challenges, and historical aviation events.
