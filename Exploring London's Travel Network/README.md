# Exploring London's Travel Network using Snowflake 🚆


### Problem 
London, or as the Romans called it "Londonium"! Home to over 8.5 million residents who speak over 300 languages. While the City of London is a little over one square mile (hence its nickname "The Square Mile"), Greater London has grown to encompass 32 boroughs spanning a total area of 606 square miles!
<br><br>
![image](https://github.com/tejal04/SQLprojects/assets/24776826/a7efd756-0f29-4fdc-9091-caa80f8af616) 

Given the city's roads were originally designed for horse and cart, this area and population growth has required the development of an efficient public transport system! Since the year 2000, this has been through the local government body called Transport for London, or TfL, which is managed by the London Mayor's office. Their remit covers the London Underground, Overground, Docklands Light Railway (DLR), buses, trams, river services (clipper and Emirates Airline cable car), roads, and even taxis.


### Data
The Mayor of London's office make their data available to the public [here](https://data.london.gov.uk/dataset). In this project, we will work with a slightly modified version of a dataset containing information about public transport journey volume by transport type.

The data has been loaded into a Snowflake database called TFL with a single table called JOURNEYS, including the following data:

#### TFL.JOURNEYS
| Column | Definition | Data type |
|--------|------------|-----------|
| `MONTH`| Month in number format, e.g., `1` equals January | `INTEGER` |
| `YEAR` | Year | `INTEGER` |
| `DAYS` | Number of days in the given month | `INTEGER` |
| `REPORT_DATE` | Date that the data was reported | `DATE` |
| `JOURNEY_TYPE` | Method of transport used | `VARCHAR` |
| `JOURNEYS_MILLIONS` | Millions of journeys, measured in decimals | `FLOAT` |

### Analysis

1. Distribution of journeys over different transportation
````sql
SELECT JOURNEY_TYPE, 
	SUM(JOURNEYS_MILLIONS) as TOTAL_JOURNEYS_MILLIONS
FROM TFL.JOURNEYS
GROUP BY JOURNEY_TYPE
ORDER BY TOTAL_JOURNEYS_MILLIONS DESC;
````
<img width="1033" alt="image" src="https://github.com/tejal04/SQLprojects/assets/24776826/b2630c7c-8cd3-45d9-9f18-2d22aeb98fc7">

Insights :
- Buses are by far the most utilized mode of transportation, with a total of over 24,905 million journeys. This highlights the central role of buses in London's public transport system, likely due to their extensive coverage and accessibility.
- The "Underground & DLR" category has the second-highest total journeys. This mode is often a backbone for commuting within the city.
- The "Overground" category has a considerable number of journeys but less compared to above two, probably because of its limited coverage.
- "TfL Rail" and "Tram" services have lower total journeys compared to other modes, indicating that these modes may serve specific purposes or have more limited coverage.
- The "Emirates Airline" has the lowest total journeys as it is expensive and not suitable for local transport.
<br><br>

2. Emirates Airline Popularity Over Time
````sql
SELECT MONTH, 
	YEAR, 
	ROUND(JOURNEYS_MILLIONS,2) AS ROUNDED_JOURNEYS_MILLIONS
FROM TFL.JOURNEYS
WHERE JOURNEY_TYPE = 'Emirates Airline' AND ROUNDED_JOURNEYS_MILLIONS IS NOT NULL
ORDER BY ROUNDED_JOURNEYS_MILLIONS DESC
LIMIT 5;
````
<img width="1051" alt="image" src="https://github.com/tejal04/SQL-projects/assets/24776826/2c968357-b6b2-403b-99b9-92d3a94a3fcf">

Insights :
- Data ranges from 2010 to 2022.
- May 2012 has the highest journeys, followed by June 2012, April 2012, May 2013, and May 2015.
- After Top 3, the values are in varies in the range 0.19 - 0.11 millions for 70 entries.
- Let's look into recent travel history [2020,2021,2022] to get better insights.
  
````sql
SELECT MONTH, 
	YEAR, 
	ROUND(JOURNEYS_MILLIONS,2) AS ROUNDED_JOURNEYS_MILLIONS
FROM TFL.JOURNEYS
WHERE YEAR IN (2021,2020,2022) AND JOURNEY_TYPE = 'Emirates Airline' AND ROUNDED_JOURNEYS_MILLIONS IS NOT NULL
ORDER BY ROUNDED_JOURNEYS_MILLIONS DESC;
````
<img width="1051" alt="image" src="https://github.com/tejal04/SQL-projects/assets/24776826/154deb71-7ef1-4252-bd3f-413ebd668b78">

Insights :
- May and June months of 2021 and 2022 performed better than other months.
- 2020 had less number of journeys, even in the peak months of May and June.
     
<br><br>

3. Least Popular Years for Tube 
````sql
SELECT 
	JOURNEY_TYPE,
	YEAR,
	SUM(JOURNEYS_MILLIONS) as TOTAL_JOURNEYS_MILLIONS
FROM TFL.JOURNEYS
WHERE JOURNEY_TYPE LIKE '%Underground%'
GROUP BY YEAR, JOURNEY_TYPE
ORDER BY TOTAL_JOURNEYS_MILLIONS ASC;
````
<img width="1053" alt="image" src="https://github.com/tejal04/SQL-projects/assets/24776826/38e5bdfb-adbe-469a-a32c-03cd55eb787f">

Insights :
- The total number of journeys for the "Underground & DLR" journey type has shown downward curve from 2010 to 2022.
- Looking at the historical trend, the number of journeys has significantly decreased in 2020-2021. The most significant factor impacting travel patterns and public transportation in 2020 was the global COVID-19 pandemic. Looks like lockdowns, social distancing measures, and restrictions on movement led to a substantial decline in overall travel, including the use of public transportation.
As the lockdowns opened up, the we can observe increase in journey counts in the consecutive years 2021-2022.
<br><br>
