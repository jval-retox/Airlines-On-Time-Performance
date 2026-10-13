# Airline On-Time Performance Data
## by Jiri Valenta


## Dataset

The dataset **"Airline On-Time Performance Data"** reports flights in the United States, including carriers, arrival and departure delays, and reasons for the delays, from 1987 to 2008. The data is collected by the Office of Airline Information, Bureau of Transportation Statistics (BTS). The original dataset is large: there are nearly 120 million records in total, and takes up 1.6 gigabytes of space compressed and 12 gigabytes when uncompressed. To speed up my analysis I extracted just 10,000 sample rows from each file, producing the final CSV file of 25 megabytes.

## Summary of Findings

The univariate visualization of the main variables revealed some interesting distributions of delays and cancellations over various timeframes, e.g. years, months, days. The frequency of flights per hours during a day showed the busiest hours for the airports. The average monthly frequency of cancellations revealed an unusual peak for September which, as investigated further, was caused by the disruptions during the events of September 2001. This single month had relatively big impact to the whole statistics.

In the bivariate exploratory visualization section I noticed an interesting relation between the departure and arrival delays and also analysed some trends in delay reason codes throughout the years. 

In multivariate part I added `AirTime` variable into the delay / arrival delay scatter plot to see whether there is additional relation. In the last part I focused on airlines's performance in terms of delays.


## Key Insights for Presentation

For the final presentation I selected four explanatory visualisations: 

1. Frequency of cancellations for selected periods: months + detailed daily bar chars for September 2001.
2. Busy hours for airports: to see which hours per day are the most busy for airlines' operations.
3. The main reasons for the delays: showing also the trends throughout the years
4. The best performing airline in terms of departure and arrival delays (e.g. early departures/arrivals)

