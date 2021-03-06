
## Revising Aggregation - The Count Function

Query a count of the number of cities in CITY having a Population larger than 100000.

Input Format

The CITY table is described as follows:

| Field | Type |
| --- | --- |
| ID | NUMBER |
| NAME | VARCHAR2(17) |
| COUNTRYCODE | VARCHAR2(3) |
| DISTRICT | VARCHAR2(20) |
| POPULATION | NUMBER |

`````sql
select
    count(name)
from city
where population > 100000;
`````
## Revising Aggregation -  The Sum Function

Query the total population of all cities in CITY where District is California.

Input Format

The CITY table is described as follows:

| Field | Type |
| --- | --- |
| ID | NUMBER |
| NAME | VARCHAR2(17) |
| COUNTRYCODE | VARCHAR2(3) |
| DISTRICT | VARCHAR2(20) |
| POPULATION | NUMBER |

`````sql
select
    sum(population)
from city
where district = 'California';
`````

## Revising Aggregations - Averages

Query the average population of all cities in CITY where District is California.

Input Format

The CITY table is described as follows:

| Field | Type |
| --- | --- |
| ID | NUMBER |
| NAME | VARCHAR2(17) |
| COUNTRYCODE | VARCHAR2(3) |
| DISTRICT | VARCHAR2(20) |
| POPULATION | NUMBER |

`````sql
select
    avg(population)
from city
where district = 'California';
`````

## Average Population

Query the average population for all cities in CITY, rounded down to the nearest integer.

Input Format

The CITY table is described as follows:

| Field | Type |
| --- | --- |
| ID | NUMBER |
| NAME | VARCHAR2(17) |
| COUNTRYCODE | VARCHAR2(3) |
| DISTRICT | VARCHAR2(20) |
| POPULATION | NUMBER |

````sql
select
    round(avg(population))
from city;
````

## Japan Population

Query the sum of the populations for all Japanese cities in CITY. The COUNTRYCODE for Japan is JPN.

Input Format

The CITY table is described as follows:

| Field | Type |
| --- | --- |
| ID | NUMBER |
| NAME | VARCHAR2(17) |
| COUNTRYCODE | VARCHAR2(3) |
| DISTRICT | VARCHAR2(20) |
| POPULATION | NUMBER |


````sql
select
    sum(population)
from city
where countrycode = 'JPN';
````

## Population Density Difference

Query the difference between the maximum and minimum populations in CITY.

Input Format

The CITY table is described as follows:

| Field | Type |
| --- | --- |
| ID | NUMBER |
| NAME | VARCHAR2(17) |
| COUNTRYCODE | VARCHAR2(3) |
| DISTRICT | VARCHAR2(20) |
| POPULATION | NUMBER |

````sql
select
    max(population) - min(population) 
from city;
````

## The Blunder

Samantha was tasked with calculating the average monthly salaries for all employees in the EMPLOYEES table, but did not realize her keyboard's 0 
key was broken until after completing the calculation. She wants your help finding the difference between her miscalculation (using salaries with
any zeros removed), and the actual average salary.

Write a query calculating the amount of error (i.e.: actual - miscalculated average monthly salaries), and round it up to the next integer.

Input Format

The EMPLOYEES table is described as follows:

| Column | Type |
| --- | --- |
| ID | Integer |
| Name | String |
| Salary | Integer |

Note: Salary is per month.

Constraints

1000 < Salary < 10??5

Sample Input

| ID | Name | Salary |
| --- | --- | --- |
| 1 | Kristeen | 1420 |
| 2 | Ashley | 2006 |
| 3 | Julia | 2210 |
| 4 | Maria | 3000 |

````sql
select
    round(avg(salary))- round(avg(replace(salary, 0, '')))
from employees;
````

## Top Earners

We define an employee's total earnings to be their monthly salary x months worked, and the maximum total earnings to be the maximum total earnings for any
employee in the Employee table. Write a query to find the maximum total earnings for all employees as well as the total number of employees 
who have maximum total earnings. Then print these values as 2 space-separated integers.

Input Format

The Employee table containing employee data for a company is described as follows:

| Column | Type |
| --- | --- |
| employee_id | Integer |
| name | String |
| months | Integer |
| salary | Integer |

Where employee_id is an employee's ID number, name is their name, months is the total number of months they've been working for the company,
and salary is the their monthly salary.

Sample Input

| employee_id | name | months | salary |
| --- | --- | --- | --- |
| 12228 | Rose | 15 | 1968 |
| 33645 | Angela | 1 | 3443 |
| 45692 | Frank | 17 | 1608 |
| 56118 | Patrick | 7 | 1345 |
| 59725 | Lisa | 11 | 2330 |
| 74197 | Kimberly | 16 | 4372 |
| 78454 | Bonnie | 8 | 1771 |
| 83565 | Michael | 6 | 2017 |
| 98607 | Todd | 5 | 3396 |
| 99989 | Joe | 9 | 3573 |

````sql
select
    max(salary * months),
    count(name)
from employee
where salary * months = (select 
                            max(salary * months) 
                         from employee);
````

## Weather Observation Station 2

Query the following two values from the STATION table:

1. The sum of all values in LAT_N rounded to a scale of  decimal places.
2. The sum of all values in LONG_W rounded to a scale of  decimal places.

Input Format

The STATION table is described as follows:

| Field | Type |
| --- | --- |
| ID | NUMBER |
| CITY | VARCHAR2(21) |
| STATE | VARCHAR2(2) |
| LAT_N | NUMBER |
| LONG_W | NUMBER |

where LAT_N is the northern latitude and LONG_W is the western longitude.

`````sql
select
    round(sum(lat_n), 2),
    round(sum(long_w), 2)
from station;
`````

## Weather Observation Station 13

Query the sum of Northern Latitudes (LAT_N) from STATION having values greater than 38.7880 and less than 137.2345. Truncate your answer to  decimal places.

Input Format

The STATION table is described as follows:

| Field | Type |
| --- | --- |
| ID | NUMBER |
| CITY | VARCHAR2(21) |
| STATE | VARCHAR2(2) |
| LAT_N | NUMBER |
| LONG_W | NUMBER |

`````sql
select
    round(sum(lat_n), 4) 
from station
where lat_n > 38.7880 and lat_n < 137.2345;

``````

## Weather Observation Station 14 

Query the greatest value of the Northern Latitudes (LAT_N) from STATION that is less than 137.2345. Truncate your answer to 4 decimal places.

Input Format

The STATION table is described as follows:

| Field | Type |
| --- | --- |
| ID | NUMBER |
| CITY | VARCHAR2(21) |
| STATE | VARCHAR2(2) |
| LAT_N | NUMBER |
| LONG_W | NUMBER |

`````sql
select
    round(max(lat_n), 4)
from station
where lat_n < 137.2345;
`````

## Weather Observation Station 15

Query the Western Longitude (LONG_W) for the largest Northern Latitude (LAT_N) in STATION that is less than 137.2345. Round your answer to 4 decimal places.

Input Format

The STATION table is described as follows:

| Field | Type |
| --- | --- |
| ID | NUMBER |
| CITY | VARCHAR2(21) |
| STATE | VARCHAR2(2) |
| LAT_N | NUMBER |
| LONG_W | NUMBER |

`````sql
select
    round(long_w, 4)
from station
where lat_n = (select
                  max(lat_n)
                from station
                where lat_n < 137.2345);

`````

## Weather Observation Station 16

Query the smallest Northern Latitude (LAT_N) from STATION that is greater than 38.7780. Round your answer to 4 decimal places.

Input Format

The STATION table is described as follows:

| Field | Type |
| --- | --- |
| ID | NUMBER |
| CITY | VARCHAR2(21) |
| STATE | VARCHAR2(2) |
| LAT_N | NUMBER |
| LONG_W | NUMBER |


````sql
select
    round(min(lat_n), 4)
from station
where lat_n > 38.7780;

````
## Weather Observation Station 17

Query the Western Longitude (LONG_W)where the smallest Northern Latitude (LAT_N) in STATION is greater than 38.7780. Round your answer to 4 decimal places.

Input Format

The STATION table is described as follows:

| Field | Type |
| --- | --- |
| ID | NUMBER |
| CITY | VARCHAR2(21) |
| STATE | VARCHAR2(2) |
| LAT_N | NUMBER |
| LONG_W | NUMBER |

`````sql
select
    round(long_w, 4)
from station
where lat_n = (select
                  min(lat_n)
               from station
               where lat_n > 38.7780);
`````

## Weather Observation Station 18

Consider P1(a,b) and P2(c,d) to be two points on a 2D plane.

- _a_ happens to equal the minimum value in Northern Latitude (LAT_N in STATION).
- _b_ happens to equal the minimum value in Western Longitude (LONG_W in STATION).
- _c_ happens to equal the maximum value in Northern Latitude (LAT_N in STATION).
- _d_ happens to equal the maximum value in Western Longitude (LONG_W in STATION).
- 
Query the Manhattan Distance between points P1 and P2 and round it to a scale of  decimal places.

Input Format

The STATION table is described as follows:

| Field | Type |
| --- | --- |
| ID | NUMBER |
| CITY | VARCHAR2(21) |
| STATE | VARCHAR2(2) |
| LAT_N | NUMBER |
| LONG_W | NUMBER |

`````sql
select 
     round(abs(max(lat_n) - min(lat_n)) + abs(max(long_w) - min(long_w)), 4)
from station;
`````

## Weather Observation Station 19

Consider P1(a,c) and P2(b,d) to be two points on a 2D plane where (a,b) are the respective minimum and maximum values of Northern Latitude (LAT_N) and (c,d) are the respective minimum and maximum values of Western Longitude (LONG_W) in STATION.

Query the Euclidean Distance between points P1 and P2 and format your answer to display  decimal digits.

Input Format

The STATION table is described as follows:

| Field | Type |
| --- | --- |
| ID | NUMBER |
| CITY | VARCHAR2(21) |
| STATE | VARCHAR2(2) |
| LAT_N | NUMBER |
| LONG_W | NUMBER |

`````sql
select 
     round(sqrt(pow(max(lat_n) - min(lat_n), 2) + pow(max(long_w) - min(long_w), 2)), 4)
from station;
``````





