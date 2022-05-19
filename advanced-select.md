## Type of Triangle

Write a query identifying the type of each record in the TRIANGLES table using its three side lengths. Output one of the following statements for each record in the table:

Equilateral: It's a triangle with 3 sides of equal length.
Isosceles: It's a triangle with 2 sides of equal length.
Scalene: It's a triangle with 3 sides of differing lengths.
Not A Triangle: The given values of A, B, and C don't form a triangle.
Input Format

The TRIANGLES table is described as follows:

| Column | Type |
| --- | --- |
| A | Integer |
| B | Integer |
| C | Integer |

Each row in the table denotes the lengths of each of a triangle's three sides.

Sample Input

| A | B | C |
| --- | --- | --- |
| 20 | 20 | 23 |
| 20 | 20 | 20 |
| 20 | 21 | 22 |
| 13 | 14 | 30 |

````sql
select
    case 
    when A + B <= C or B + C <= A or C + A <= B then 'Not A Triangle'
    when A = B and B = C then 'Equilateral'
    when A = B or B = C or C = A then 'Isosceles'
    when A != B and B != C then 'Scalene'
    end as triangle
from triangles;
````

## The PADS

Generate the following two result sets:

Query an alphabetically ordered list of all names in OCCUPATIONS, immediately followed by the first letter of each profession as a parenthetical (i.e.: enclosed in parentheses). For example: AnActorName(A), ADoctorName(D), AProfessorName(P), and ASingerName(S).
Query the number of ocurrences of each occupation in OCCUPATIONS. Sort the occurrences in ascending order, and output them in the following format:

````
There are a total of [occupation_count] [occupation]s.
`````

where [occupation_count] is the number of occurrences of an occupation in OCCUPATIONS and [occupation] is the lowercase occupation name. If more
than one Occupation has the same [occupation_count], they should be ordered alphabetically.

Note: There will be at least two entries in the table for each type of occupation.

Input Format

| Column | Type |
| --- | --- |
| Name | String |
| Occupation | String |

The OCCUPATIONS table is described as follows:
Occupation will only contain one of the following values: Doctor, Professor, Singer or Actor.

Sample Input

An OCCUPATIONS table that contains the following records:

| Name | Occupation |
| --- | --- |
| Samantha | Doctor |
| Julia | Actor |
| Maria | Actor |
| Meera | Singer |
| Ashely | Professor |
| Ketty | Professor |
| Christeen | Professor |
| Jane | Actor |
| Jenny | Doctor |
| Priya | Singer |

`````sql
select 
    concat(name,'(',upper(substring(occupation,1,1)),')')
from occupations
order by name;

select 
    concat("There are a total of",
           ' ',
           count(occupation),
           ' ',
           lower(occupation),'s',".")  
from occupations
group by occupation
order by count(occupation);

````


