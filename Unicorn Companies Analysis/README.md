# Unicorn Companies Analysis 🦄 


### Problem : 
You have been asked to support an investment firm by analyzing trends in high-growth companies. They are interested in understanding which industries are producing the highest valuations and the rate at which new high-value companies are emerging. Providing them with this information gives them a competitive insight as to industry trends and how they should structure their portfolio looking forward.

### Data : 
Given Unicorn Database that contains 4 tables :
- dates
- funding
- industries
- companies

#### dates
| Column       | Description                                  |
|------------- |--------------------------------------------- |
| `company_id`   | A unique ID for the company.                 |
| `date_joined` | The date that the company became a unicorn.  |
| `year_founded` | The year that the company was founded.       |

#### funding
| Column           | Description                                  |
|----------------- |--------------------------------------------- |
| `company_id`       | A unique ID for the company.                 |
| `valuation`        | Company value in US dollars.                 |
| `funding`          | The amount of funding raised in US dollars.  |
| `select_investors` | A list of key investors in the company.      |

#### industries
| Column       | Description                                  |
|------------- |--------------------------------------------- |
| `company_id`   | A unique ID for the company.                 |
| `industry`     | The industry that the company operates in.   |

#### companies
| Column       | Description                                       |
|------------- |-------------------------------------------------- |
| `company_id`   | A unique ID for the company.                      |
| `company`      | The name of the company.                          |
| `city`         | The city where the company is headquartered.      |
| `country`      | The country where the company is headquartered.   |
| `continent`    | The continent where the company is headquartered. |


### Analysis :

1. How many unique companies exist in the dataset?

````sql
SELECT 
  COUNT(DISTINCT company_id) AS unique_companies
FROM companies
````
<img width="488" alt="image" src="https://github.com/tejal04/SQLprojects/assets/24776826/1967c101-89d9-4c3b-b947-1997d39fa6d1">
<br> <br>

2. How many industries exist in the dataset?
````sql
SELECT 
  COUNT(DISTINCT industry) AS unique_industries
FROM industries
````
<img width="488" alt="image" src="https://github.com/tejal04/SQLprojects/assets/24776826/37f08da4-1407-4109-b97d-d310be2b9c2e">
<br> <br>

3. Find the unicorn company with the highest valuation?
````sql
SELECT f.company_id,  c.company, f.valuation
FROM funding AS f
JOIN companies AS c ON f.company_id = c.company_id
ORDER BY f.valuation DESC
LIMIT 1;
````
<img width="488" alt="image" src="https://github.com/tejal04/SQLprojects/assets/24776826/ec1734b5-f44b-42f4-830a-90dffd02562d">
<br> <br>

4. Find the top 10 unicorn companies with the highest valuations?
````sql
SELECT c.company, f.valuation
FROM companies AS c
JOIN funding AS f ON c.company_id = f.company_id
ORDER BY f.valuation DESC
LIMIT 10; 
````
<img width="488" alt="image" src="https://github.com/tejal04/SQLprojects/assets/24776826/12341775-f4cc-42c8-944b-b11a78b679e5">
<br> <br>

5. Distribution of unicorn companies over industries?
````sql
SELECT industry,
       COUNT(DISTINCT company_id) AS num_unicorns
FROM industries
GROUP BY industry
ORDER BY num_unicorns DESC;
````
<img width="488" alt="image" src="https://github.com/tejal04/SQLprojects/assets/24776826/64428cbf-7e19-4193-89ec-649f9ec1d181">
<br> <br>

6. Calculate the total funding raised each year?
````sql
SELECT EXTRACT(YEAR FROM date_joined) AS funding_year,
       SUM(funding) AS total_funding_amount
FROM dates
JOIN funding ON dates.company_id = funding.company_id
GROUP BY funding_year
ORDER BY funding_year;
````
<img width="488" alt="image" src="https://github.com/tejal04/SQLprojects/assets/24776826/fba6c07b-03e3-4de6-acd4-67b449081ed7">
<br> <br>

7. Distribution of unicorn companies over industries?
````sql
SELECT EXTRACT(YEAR FROM date_joined) AS joining_year,
       COUNT(DISTINCT company_id) AS num_unicorns
FROM dates
GROUP BY joining_year
ORDER BY joining_year;
````
<img width="488" alt="image" src="https://github.com/tejal04/SQLprojects/assets/24776826/72b6e692-2861-45e1-aafb-8d672d089d21">
<br> <br>

8. Find the countries with the most unicorn companies?
````sql
SELECT country, COUNT(DISTINCT company_id) AS num_unicorns
FROM companies
GROUP BY country
ORDER BY num_unicorns DESC;
````
<img width="488" alt="image" src="https://github.com/tejal04/SQLprojects/assets/24776826/272e4527-124d-43da-a6e8-f822931235bb">
<br> <br>

9. Find the cities with the most unicorn companies?
````sql
SELECT city, country, COUNT(DISTINCT company_id) AS num_unicorns
FROM companies
GROUP BY city,country
ORDER BY num_unicorns DESC;
````
<img width="488" alt="image" src="https://github.com/tejal04/SQLprojects/assets/24776826/8e5feadb-ecfb-4132-bf81-0c5d5eb2ee4f">
<br> <br>

10. Distribution unicorn companies over continents?
````sql
SELECT continent, COUNT(DISTINCT company_id) AS num_unicorns
FROM companies
GROUP BY continent
ORDER BY num_unicorns DESC;
````
<img width="488" alt="image" src="https://github.com/tejal04/SQLprojects/assets/24776826/c843a7b9-0dc1-48c6-8d5e-9dfca2169bff">
<br> <br>


