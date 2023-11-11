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
2. 
