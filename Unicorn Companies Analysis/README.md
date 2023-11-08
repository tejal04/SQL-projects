# Unicorn Companies Analysis 🦄 


### Problem : 
You have been asked to support an investment firm by analyzing trends in high-growth companies. They are interested in understanding which industries are producing the highest valuations and the rate at which new high-value companies are emerging. Providing them with this information gives them a competitive insight as to industry trends and how they should structure their portfolio looking forward.

### Data : 
Given Unicorn Database that contains 4 tables :
- dates
- fundings
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
FROM public.companies
````
<img width="488" alt="image" src="https://github.com/tejal04/SQLprojects/assets/24776826/1967c101-89d9-4c3b-b947-1997d39fa6d1">
<br> <br>

2. How many industries exist in the dataset?
````sql
SELECT 
  COUNT(DISTINCT industry) AS unique_industries
FROM public.industries
````
<img width="488" alt="image" src="https://github.com/tejal04/SQLprojects/assets/24776826/37f08da4-1407-4109-b97d-d310be2b9c2e">
<br> <br>

3. 

