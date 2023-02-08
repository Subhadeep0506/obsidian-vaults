# 1. Most popular movie category
**Instruction**
-   Return the name of the category that has the most films.
-   If there are ties, return just one of them.

#### Table 1: category sample data

Movie categories.

|col_name |col_type|
|---|---|
|category_id | integer|
|name| text|

#### Table 2: film_category sample data

A film can only belong to one category

 | col_name   | col_type|
  |---|---|
| film_id     | smallint|
| category_id | smallint|

Sample results

| name | |
|---|---|
|Category Name| |

### Solution:
```sql
select name from category as a
inner join film_category as b using(category_id)
where a.category_id = (
	select category_id from film_category
  	group by category_id order by count(*) desc Limit 1
) Limit 1;
```

# 2. Films that are in stock vs not in stock
**Instruction**

-   Write a query to return the number of films that we have inventory vs no inventory.
-   A film can have multiple inventory ids
-   Each film DVD copy has a unique inventory ids

#### Table 1: film sample data

|col_name|col_type|
|---|---|
|film_id | integer
|title                | text
|description          | text
|release_year         | integer
|language_id          | smallint
|original_language_id | smallint
|rental_duration      | smallint
|rental_rate          | numeric
|length               | smallint
|replacement_cost     | numeric
|rating               | text

#### Table 2: inventory sample data

Each row is unique, `inventoy_id` is the primary key of this table.

|col_name   | col_type|
|---|---|
|inventory_id | integer
|film_id      | smallint
|store_id     | smallint

#### Sample results

|in_stock| count|
|---|---|
|in stock     |   123
|not in stock |    456

### Solution
```sql
SELECT in_stock,
COUNT(*) as count
FROM (
  SELECT a.film_id,
  CASE WHEN COUNT(b.inventory_id) > 0 THEN 'in stock'
  ELSE 'not in stock'
  END as in_stock
  FROM film a 
  LEFT JOIN inventory b USING(film_id)
  GROUP BY a.film_id
) c
GROUP BY in_stock;
```

# 3. Customers who rented vs. those who did not
**Instruction**
-   Write a query to return the number of customers who rented at least one movie vs. those who didn't in **May 2020**.
-   The order of your results doesn't matter.
-   Use `customer` table as the base table for all customers (assuming all customers have signed up before May 2020)
-   `Rented`: if a customer rented at least one movie.
-   **Bonus:** Develop a `LEFT JOIN` as well as a `RIGHT JOIN` solution

#### Table 1: customer sample data

|col_name   | col_type|
|---|---|
|customer_id | integer
|store_id    | smallint
|first_name  | text
|last_name   | text
|email       | text
|address_id  | smallint
|activebool  | boolean
|create_date | date
|active      | integer

#### Table 2: rental sample data

|col_name   | col_type|
|---|---|
|rental_id    | integer
|rental_ts    | timestamp with time zone
|inventory_id | integer
|customer_id  | smallint
|return_ts    | timestamp with time zone
|staff_id     | smallint

#### Sample results

|hass_rented | count|
|---|---|
|rented      |   123
|never-rented  |   456

### Solution
```sql
SELECT rented, COUNT(*) 
FROM (
	SELECT DISTINCT c.customer_id,
  	CASE WHEN COUNT(r.rental_id) > 0 THEN 'rented'
  	ELSE 'never-rented'
  	END as rented
  	FROM customer c
  	LEFT JOIN rental r 
  	on c.customer_id = r.customer_id and
  	EXTRACT(month from r.rental_ts) = 5 and 
  	EXTRACT(year from r.rental_ts) = 2020
  	GROUP BY c.customer_id
) temp
GROUP BY rented;
```

# 4. The PADS
Generate the following two result sets:

1.  Query an _alphabetically ordered_ list of all names in **OCCUPATIONS**, immediately followed by the first letter of each profession as a parenthetical (i.e.: enclosed in parentheses). For example: `AnActorName(A)`, `ADoctorName(D)`, `AProfessorName(P)`, and `ASingerName(S)`.
2.  Query the number of occurrences of each occupation in **OCCUPATIONS**. Sort the occurrences in _ascending order_, and output them in the following format:  
    
    ```
    There are a total of [occupation_count] [occupation]s.
    ```
    
    where `[occupation_count]` is the number of occurrences of an occupation in **OCCUPATIONS** and `[occupation]` is the _lowercase_ occupation name. If more than one _Occupation_ has the same `[occupation_count]`, they should be ordered alphabetically.
    

**Note:** There will be at least two entries in the table for each type of occupation.

**Input Format**

The **OCCUPATIONS** table is described as follows:
![](https://s3.amazonaws.com/hr-challenge-images/12889/1443816414-2a465532e7-1.png)_Occupation_ will only contain one of the following values: **Doctor**, **Professor**, **Singer** or **Actor**.

**Sample Input**

An **OCCUPATIONS** table that contains the following records:

![](https://s3.amazonaws.com/hr-challenge-images/12889/1443816608-0b4d01d157-2.png)

**Sample Output**

```
Ashely(P)
Christeen(P)
Jane(A)
Jenny(D)
Julia(A)
Ketty(P)
Maria(A)
Meera(S)
Priya(S)
Samantha(D)
There are a total of 2 doctors.
There are a total of 2 singers.
There are a total of 3 actors.
There are a total of 3 professors.
```

**Explanation**

The results of the first query are formatted to the problem description's specifications.  
The results of the second query are ascendingly ordered first by number of names corresponding to each profession (2<=2<=3<=3), and then alphabetically by profession (doctor<= singer)

```sql
SELECT CONCAT(Name, '(',SUBSTRING(Occupation,1,1) ,')') as Name
FROM OCCUPATIONS ORDER BY Name ASC;

SELECT CONCAT('There are a total of ',COUNT(Occupation) ,' ', lower(Occupation), 's.') 
FROM OCCUPATIONS 
GROUP BY Occupation
ORDER BY COUNT(Occupation), Occupation ASC;
```

# 5. Number Of Units Per Nationality
Find the number of apartments per nationality that are owned by people under 30 years old. Output the nationality along with the number of apartments. Sort records by the apartments count in descending order.

**Tables: airbnb_hosts, airbnb_units**

### airbnb_hosts
```
host_id:int
nationality:varchar
gender:varchar
age:int
```

### airbnb_units
```
host_id:int
unit_id:varchar
unit_type:varchar
n_beds:int
n_bedrooms:int
country:varchar
city:varchar
```

### Solution:
```sql
select h.nationality, count(distinct u.unit_id) as apartment_count
from airbnb_units u
join airbnb_hosts h on h.host_id = u.host_id
where h.age < 30 and u.unit_type = 'Apartment'
group by u.host_id, h.nationality
order by apartment_count desc;
```

# 5. Ranking Most Active Guests
Rank guests based on the number of messages they've exchanged with the hosts. Guests with the same number of messages as other guests should have the same rank. Do not skip rankings if the preceding rankings are identical. Output the rank, guest id, and number of total messages they've sent. Order by the highest number of total messages first.

**Table: airbnb_contacts**

### airbnb_contacts

```
id_guest:varchar
id_host:varchar
id_listing:varchar
ts_contact_at:datetime
ts_reply_at:datetime
ts_accepted_at:datetime
ts_booking_at:datetime
ds_checkin:datetime
ds_checkout:datetime
n_guests:int
n_messages:int
```

### Solution:
```sql
select 
dense_rank() over(order by sum(n_messages) desc) as ranking,
id_guest, sum(n_messages)
from airbnb_contacts
group by id_guest
order by sum(n_messages) desc;
```

