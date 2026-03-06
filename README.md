# NYC 311 Service Request Analysis

## Overview
This repository analyzes 6.5 million NYC 311 service requests collected between January 1, 2024 and December 31, 2025. It explores how response times and request patterns vary between boroughs, NYC agencies, and zip codes, and whether neighrborhood demographics are associated with differences in city responsiveness. This data was collected from the [NYC 311 Open Data Portal](https://data.cityofnewyork.us/Social-Services/NYC-311-Data/jrb2-thup/about_data) and demographic data from the US Census Bureau.

## Key Findings
1. **Response times vary significantly between boroughs** (Kruskal-Wallis, p < 0.001). Manhattan is the slowest to respond (average 12.6 days), while the Bronx is the fastes (average 7.1 days).
2. **Response times vary significantly between city agencies** (Kruskal-Wallis, p < 0.001). The NYPD takes an average of 7 minutes to respond to a request, while the Economic Development Corporation (EDC) takes over 100 days.
3. **Request type matters within agencies.** Every agency shows a significant variability in response time across complaint types (Kruskal-Wallis / Wilcoxon Rank-Sums, p < 0.001). For example, the Parks Department tends to resolve park rule violations in under a day, but 308 days to respond to a new tree request.
4. **Zip code 11430 (JFK) is a notable outlier**. 90% of requests in this zip code are associated with the Taxi and Limo Commission. This is likely due to its nature as an international airport rather than a residental area.
5. **A zip code's demographics relate to the number of requests it submits, but not the time it takes the city to respond.** Zip codes with higher proportions of Black residents (p = 0.021), Hispanic residents (p < 0.001), and residents with bachelor's degrees (p < 0.001) submitted more requests. However, no single demographic had a significant relationship to the response time, although the overall model was significant (F = 3.41, p = 0.002), indicating the question should be continued to be analyzed.

## Dashboard
An interactive Tabluea dashboard summarizing key findings is avilable [here](https://public.tableau.com/app/profile/matthew.clark6642/viz/NYC311_17728249450880/ResponseTimes).

## Research Questions
- **RQ1:** How does response time vary between boroughs and agencies?
- **RQ2:** How does the frequency of requests to each agency vary between locations?
- **RQ3:** What complaint types within each agency have the highest response times?
- **RQ4:** How does a zip code's demographics relate to the number of submitted requests and response time?

## Methodology
- Data was stored and queried using **PostgreSQL**
- Statistical testing: **Kruskal-Wallis**, **Wilcoxon Rank-Sums**, and **Chi-Squared** tests
- Demographic relationships modeled using **OLS regression**
- Visualizations were built using **Plotly**

## Tools Used
- Python
- PostgreSQL
- panas
- NumPy
- SciPy
- statsmodels
- Plotly

## How to Run
1. Clone the repo
2. Set up a PostgreSQL database and load the NYC 311 data and census data
3. Install dependencies from `requirements.txt`
4. Run `nyc311_analysis.ipynb`