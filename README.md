# NYC 311 Service Request Analysis

## Overview
This repository analyzes 6.5 million NYC 311 service requests collected between January 1, 2024 and December 31, 2025. It explores how response times and request patterns vary between boroughs, NYC agencies, and zip codes, and whether neighborhood demographics are associated with differences in city responsiveness. This data was collected from the [NYC 311 Open Data Portal](https://data.cityofnewyork.us/Social-Services/NYC-311-Data/jrb2-thup/about_data) and demographic data from the US Census Bureau.

## Key Findings
1. **Response times vary significantly between boroughs** (Kruskal-Wallis, p < 0.001). Manhattan is the slowest to respond (average 12.6 days), while the Bronx is the fastest (average 7.1 days).
2. **Response times vary significantly between city agencies** (Kruskal-Wallis, p < 0.001). The NYPD takes an average of 7 minutes to respond to a request, while the Economic Development Corporation (EDC) takes over 100 days.
3. **Request type matters within agencies.** Every agency shows a significant variability in response time across complaint types (Kruskal-Wallis / Wilcoxon Rank-Sums, p < 0.001). For example, the Parks Department tends to resolve park rule violations in under a day, but 308 days to respond to a new tree request.
4. **Zip code 11430 (JFK) is a notable outlier**. 90% of requests in this zip code are associated with the Taxi and Limo Commission. This is likely due to its nature as an international airport rather than a residential area.
5. **A zip code's demographics relate to the number of requests it submits, but not the time it takes the city to respond.** Zip codes with higher proportions of Black residents (p = 0.021), Hispanic residents (p < 0.001), and residents with bachelor's degrees (p < 0.001) submitted more requests. However, no single demographic had a significant relationship to the response time, although the overall model was significant (F = 3.41, p = 0.002), suggesting that demographic composition has a collective effect that warrants deeper investigation, potentially with interaction terms or neighborhood clustering approaches. 

## Dashboard
An interactive Tableau dashboard summarizing key findings is avialable [here](https://public.tableau.com/app/profile/matthew.clark6642/viz/NYC311_17728249450880/ResponseTimes). 

The dashboard contains 3 pages:
- **Response Time by Borough/Agency**: Borough and agency-level response time comparisons. Manhattan is the slowest borough to respond (12.6 days on average). The NYPD resolves requests in minutes while the EDC averages over 100 days.
- **Request Distribution and Response Time by Zip Codes**: Choropleth maps and a heatmap showing geographic variation in volume and response time. Highlights outliers like zip code 11430 (JFK airport), where 90% of requests go to the Taxi & Limousine Commission.
- **Request Distribution and Response Time by Zip Code Demographics**: Scatter plots exploring relationships between neighborhood demographics and 311 engagement.

## Methodology
- **Data pipeline**: 6.5M service requests stored and queried using **PostgreSQL**; analysis conducted in **Python** (**Pandas**, **NumPy**, **SciPy**, **statsmodels**)
- **Response time analysis**: **Kruskal-Wallis** and **Wilcoxon Rank-Sums** used to compare distributions across boroughs, agencies, and complaint types
- **Outlier analysis**: **Chi-Squared** tests used to identify anomalous request distributions by zip code (e.g., zip code 11430 / JFK airport) 
- **Demographic modeling**: **OLS regrssion** used to examine relationships between zip code demographics (US Census) and both request volume and response time
- **Visualizations**: Built using **Plotly**; key findings summarized in an interactive **Tableau** dashboard.

## How to Run
1. Clone the repo
2. Set up a PostgreSQL database and load the NYC 311 data and census data
3. Install dependencies from `requirements.txt`
4. Run `nyc311_analysis.ipynb`
