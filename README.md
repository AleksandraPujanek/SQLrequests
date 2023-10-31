# SQLrequests
Repo with helpful SQL requests.

1. Find the movies not released in the years between 2000 and 2010 (from Movie table)

![1-base-table](https://github.com/AleksandraPujanek/SQLrequests/blob/5dbec32ae2a075dfb694be2c6b9d3d2d5ecdc6b9/images/1-base-table1.png)

Solution no 1
```sql
SELECT Title, Year FROM Movies
WHERE Year < 2000 OR year > 2010;
```

Solution no 2
```sql
SELECT Title, Year FROM Movies
WHERE Year NOT BETWEEN 2000 AND 2010;
```
Output:

![1-response](https://raw.githubusercontent.com/AleksandraPujanek/SQLrequests/main/images/1-response.png)

---

2. Find all the Toy Story movies (title and director) not directed by John Lasseter (from Movie table)

![2-base-table](https://raw.githubusercontent.com/AleksandraPujanek/SQLrequests/main/images/2-base-table.png)

```sql
SELECT Title, Director FROM Movies
WHERE Title LIKE "%Toy Story%"
AND Director <> "John Lasseter";
```
Output:

![2-response](https://raw.githubusercontent.com/AleksandraPujanek/SQLrequests/main/images/2-response.png)

---

3. Find all the Toy Story sequels released after year 2000 (from Movie table)

![2-base-table](https://raw.githubusercontent.com/AleksandraPujanek/SQLrequests/main/images/2-base-table.png)

```sql
SELECT title, Year FROM Movies 
WHERE Title LIKE "Toy Story _";
```
Output:

![3-response](https://raw.githubusercontent.com/AleksandraPujanek/SQLrequests/main/images/3-response.png)

---

4. List all directors sorted alphabetically without duplicate (from Movie table)

![4-base-table](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/4-base-table.png)

```sql
SELECT DISTINCT Director FROM Movies
ORDER BY Director;
```
Output:

![4-response](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/4-response.png)

---

5. List next 3 movies released between yeasr 1995 and 2005  (from Movie table)

![5-base-table](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/5-base-table.png?raw=true)

```sql
SELECT * FROM Movies
WHERE Year BETWEEN 1995 AND 2005
ORDER BY Year
LIMIT 3 OFFSET 3;
```
Output:

![5-response2](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/5-response2.png?raw=true)

---

6. List the third and fourth largest cities (by population) in the United States and their population (from North_american_cities table)

![6-base-table](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/6-base-table.png?raw=true)

```sql
SELECT * FROM North_american_cities
WHERE Country = "United States"
ORDER BY Population DESC
LIMIT 2 OFFSET 2;
```
Output:

![6-response2](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/6-response.png?raw=true)

