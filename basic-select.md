## Revising the Select Query I

Query all columns for all American cities in the CITY table with populations larger than 100000. The CountryCode for America is USA.
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
  *
from city
where countrycode = 'USA'
      and population > 100000;
````

## Revising the Select Query II

Query the NAME field for all American cities in the CITY table with populations larger than 120000. The CountryCode for America is USA. 
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
  name
from city
where countrycode = 'USA'
      and population > 120000;
````
      
## Select All

Query all columns (attributes) for every row in the CITY table. The CITY table is described as follows:

| Field | Type |
| --- | --- |
| ID | NUMBER |
| NAME | VARCHAR2(17) |
| COUNTRYCODE | VARCHAR2(3) |
| DISTRICT | VARCHAR2(20) |
| POPULATION | NUMBER |

````sql
select
  *
from city;
````

## Select by ID

Query all columns for a city in CITY with the ID 1661. The CITY table is described as follows:

| Field | Type |
| --- | --- |
| ID | NUMBER |
| NAME | VARCHAR2(17) |
| COUNTRYCODE | VARCHAR2(3) |
| DISTRICT | VARCHAR2(20) |
| POPULATION | NUMBER |

````sql
select
  *
from city
where id = 1661;
````

## Japanese Cities Atributes

Query all attributes of every Japanese city in the CITY table. The COUNTRYCODE for Japan is JPN. The CITY table is described as follows: 

| Field | Type |
| --- | --- |
| ID | NUMBER |
| NAME | VARCHAR2(17) |
| COUNTRYCODE | VARCHAR2(3) |
| DISTRICT | VARCHAR2(20) |
| POPULATION | NUMBER |

````sql
select
  *
from city
where countrycode = 'JPN';
````

## Japanese Cities' Names

Query the names of all the Japanese cities in the CITY table. The COUNTRYCODE for Japan is JPN. The CITY table is described as follows:

| Field | Type |
| --- | --- |
| ID | NUMBER |
| NAME | VARCHAR2(17) |
| COUNTRYCODE | VARCHAR2(3) |
| DISTRICT | VARCHAR2(20) |
| POPULATION | NUMBER |

````sql
select
  name
from city
where countrycode = 'JPN';
````

## Weather Observation Station 1

Query a list of CITY and STATE from the STATION table. The STATION table is described as follows:

| Field | Type |
| --- | --- |
| ID | NUMBER |
| CITY | VARCHAR2(21) |
| STATE | VARCHAR2(2) |
| LAT_N | NUMBER |
| LONG_W | NUMBER |

````sql
select
  city,
  state
from station;
````
## Weather Observation Station 3

Query a list of CITY names from STATION for cities that have an even ID number. Print the results in any order, but exclude duplicates from the answer.
The STATION table is described as follows:

| Field | Type |
| --- | --- |
| ID | NUMBER |
| CITY | VARCHAR2(21) |
| STATE | VARCHAR2(2) |
| LAT_N | NUMBER |
| LONG_W | NUMBER |

````sql
select distinct 
  city
from station
where id % 2 = 0;
````
## Weather Observation Station 4

Find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table.
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
  count(city) - count(distinct city) 
from station;
````

## Weather Observation Station 5

Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name).
If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically. The STATION table is described as 
follows:

| Field | Type |
| --- | --- |
| ID | NUMBER |
| CITY | VARCHAR2(21) |
| STATE | VARCHAR2(2) |
| LAT_N | NUMBER |
| LONG_W | NUMBER |

````sql
select 
    min(city),
    city_length
from (select
        city,
        char_length(city) city_length,
        max(char_length(city)) over() max_length,
        min(char_length(city)) over() min_length
     from station) as c 
where city_length in (max_length, min_length)
group by city_length;
````

## Weather Observation Station 6

Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.

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
select distinct
    city
from station
where city like 'a%'
    or city like 'e%' 
    or city like 'i%'
    or city like 'o%'
    or city like 'u%'
order by 1;
````

## Weather Observation Station 7

Query the list of CITY names ending with vowels (a, e, i, o, u) from STATION. Your result cannot contain duplicates.

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
select distinct
    city
from station
where city like '%a'
    or city like '%e'
    or city like '%i'
    or city like '%o'
    or city like '%u'
order by 1;
````

## Weather Observation Station 8

Query the list of CITY names from STATION which have vowels (i.e., a, e, i, o, and u) as both their first and last characters. Your result cannot contain duplicates.

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
    city
from station
where left(city, 1) in ("a", "e", "i", "o", "u") 
    and right(city, 1) in ("a", "e", "i", "o", "u")
order by 1;
````

## Weather Observation Station 9

Query the list of CITY names from STATION that do not start with vowels. Your result cannot contain duplicates.

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
select distinct
    city
from station
where left(city, 1) not in ('a','e','i','o','u')
order by 1;
````

## Weather Observation Station 10

Query the list of CITY names from STATION that do not end with vowels. Your result cannot contain duplicates.

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
select distinct
    city
from station
where right(city, 1) not in ('a','e','i','o','u')
order by 1;
````

## Weather Observation Station 11

Query the list of CITY names from STATION that either do not start with vowels or do not end with vowels. Your result cannot contain duplicates.

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
select distinct
    city
from station
where left(city, 1) not in ('a','e','i','o','u')
      or right(city,1) not in ('a','e','i','o','u')
order by 1;
````

## Weather Observation Station 12

Query the list of CITY names from STATION that do not start with vowels and do not end with vowels. Your result cannot contain duplicates.

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
select distinct
    city
from station
where left(city, 1) not in ('a','e','i','o','u')
    and right(city, 1) not in ('a','e','i','o','u')
order by 1;
````

## Higher Than 75 Marks

Query the Name of any student in STUDENTS who scored higher than  Marks. Order your output by the last three characters of each name. If two or more students both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID.

Input Format

The STUDENTS table is described as follows:

| Column | Type |
| --- | --- |
| ID | Integer |
| NAME | String |
| MARKS | Integer |

The Name column only contains uppercase (A-Z) and lowercase (a-z) letters.

Sample Input

| ID | Name | Marks |
| --- | --- | --- |
| 1 | Ashley | 81 |
| 2 | Samantha | 75 |
| 4 | Julia | 76 |
| 3 | Belvet | 84 |

````sql
select
    name 
from students 
where marks > 75 
order by substring(name,length(name)-2, 3), id;  
 ````
 
## Employee Names

Write a query that prints a list of employee names (i.e.: the name attribute) from the Employee table in alphabetical order.

Input Format

The Employee table containing employee data for a company is described as follows:

| Column | Type |
| --- | --- |
| employee_id | Integer |
| name | String |
| months | Integer |
| salary | Integer |

Where employee_id is an employee's ID number, name is their name, months is the total number of months they've been working for the company, 
and salary is their monthly salary.

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
    name
from employee
order by 1;
````

## Employee Salaries

Write a query that prints a list of employee names (i.e.: the name attribute) for employees in Employee having a salary greater than  per month who have been employees for less than  months. Sort your result by ascending employee_id.

Input Format

The Employee table containing employee data for a company is described as follows:

| Column | Type |
| --- | --- |
| employee_id | Integer |
| name | String |
| months | Integer |
| salary | Integer |

where employee_id is an employee's ID number, name is their name, months is the total number of months they've been working for the company,
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
    name
from employee
where salary > 2000 and months < 10
order by employee_id;
````





















