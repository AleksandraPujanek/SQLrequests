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

![6-response](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/6-response.png?raw=true)

---

7. List all buildings and the distinct employee roles in each building, including empty buildings (from Buildings, Employees tables)

![7-base-table1](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/7-base-table1-2.png?raw=true)
![7-base-table2](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/7-base-table2-2.png?raw=true)

```sql
SELECT DISTINCT Building_name, Role 
FROM Buildings 
  LEFT JOIN Employees 
  ON Buildings.Building_name = Employees.Building;
```
Output:

![7-response](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/7-response.png?raw=true)

---

8. List the name of the buildings that hold no employees (from Buildings, Employees tables)

![8-base-table1](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/8-base-table1.png?raw=true)
![8-base-table2](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/8-base-table2.png?raw=true)

```sql
SELECT Building_name 
FROM Buildings
  LEFT JOIN Employees
  ON Buildings.Building_name = Employees.Building
    WHERE Building IS Null;
```
Output:

![8-response](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/8-response2.png?raw=true)

---

9. Find the longest time that an employee has been at the studio (from Employees table)

![9-base-table](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/9-base-table.png?raw=true)

Solution no 1
```sql
SELECT Years_employed as MaxYearsEmployed
FROM employees
  ORDER BY Years_employed DESC
  LIMIT 1;
```

Solution no 2
```sql
SELECT MAX(years_employed) as MaxYearsEmployed
FROM Employees;
```

Output:

![9-response](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/9-response.png?raw=true)

---

10. List the total number of years employed for each role in each building (from Employees table)

![9-base-table](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/9-base-table.png?raw=true)

```sql
SELECT Role, Building, SUM(Years_employed)
  FROM Employees
  GROUP BY Role, Building;
```
Output:

![10-response](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/10-response.png?raw=true)

---

11. Find the total domestic and international sales (rounded to million $) that can be attributed to each director (from Movies, Boxoffice tables)

![11-base-table1](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/11-base-table1.png?raw=true)
![11-base-table2](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/11-base-table2.png?raw=true)

```sql
SELECT Director, ROUND((Domestic_sales+International_sales)/1000000) as Total_sale_in_mln_$
  FROM Movies
    LEFT JOIN Boxoffice 
    ON Movies.Id = Boxoffice.Movie_id
    GROUP BY Director;
```
Output:

![11-response2](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/11-response2.png?raw=true)

---

12. Find the title and director of first five highest rated movies and their total domestic and international sales bigger than 400 mln $, rounded to million $ (from Movies, Boxoffice tables)

![11-base-table1](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/11-base-table1.png?raw=true)
![11-base-table2](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/11-base-table2.png?raw=true)

```sql
SELECT Title, Director, Rating, ROUND((Domestic_sales+International_sales)/1000000) as Total_sale_in_mln_$
  FROM Movies
    JOIN Boxoffice 
    ON Movies.Id = Boxoffice.Movie_id
      WHERE Total_sale_in_mln_$ > 400
      ORDER BY Rating DESC, Total_sale_in_mln_$ DESC
      LIMIT 5; 
```
Output:

![11-response2](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/12-response2.png?raw=true)

---

13. Add new row with "Toy Stary 4" movie. (from Movies table)
    
![13-base-table1](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/13-base-table1.png?raw=true)

Solution no 1

```sql
INSERT INTO Movies 
  VALUES (4,"Toy Story 4","John Lasseter", "2010", "92");
```
Output:

![13-response](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/13-response.png?raw=true)

Solution no 2

```sql
INSERT INTO Movies
  (Title, Year)
  VALUES ("Toy Story 4","2010");
```
Output:

![13-response](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/13-response2.png?raw=true)

---

14. Update the information for "Toy Story 4" movie. (from Movies table)
    
![14-base-table](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/14-base-table.png?raw=true)

```sql
UPDATE Movies
  SET Director = "John Lasseter", 
      Length_minutes = "92"
  WHERE Id=15;
```
Output:

![14-response](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/14-response.png?raw=true)

---

15. Delete movies released after year 2000. (from Movies table)
    
![15-base-table](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/15-base-table.png?raw=true)

```sql
DELETE FROM Movies 
  WHERE Year>2000;
```
Output:

![15-response](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/15-response.png?raw=true)

---

16. Create a table for defects and add values for it.

![16-response1](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/16-response1.png?raw=true)

```sql
CREATE TABLE IF NOT EXISTS Defects (
    Id INTEGER PRIMARY KEY,
    Reporter TEXT NOT NULL,
    Summary  TEXT NOT NULL,
    Reproduction_steps TEXT NOT NULL,
    Expected_result  TEXT NOT NULL,
    Actual_Result  TEXT NOT NULL,
    Date_Time  DATETIME NOT NULL,
    Priority  INTEGER,
    Severity  INTEGER,
    BA_Assessment TEXT
);
```
Output:

![16-response2](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/16-response2.png?raw=true)

```sql
INSERT INTO Defects 
  VALUES
    (1,"Aleksandra Pujanek","A board with name of # could not be created","Create a board with given name: #","Response Code:200 - OK, Board is created with name: #","Response Code:401 - Unauthorized","2023-10-27 10:36:47","Low","Minor","N/A"),
    (2,"Aleksandra Pujanek","A board with name of % could not be created","Create a board with given name: %","Response Code:200 - OK, Board is created with name: %","Response Code:400 - Bad Request","2023-10-27 10:36:47","Low","Minor","N/A"),
    (3,"Aleksandra Pujanek","A board with name of & could not be created","Create a board with given name: &","Response Code:200 - OK, Board is created with name: &","Response Code:400 - Bad Request","2023-10-27 10:36:47","Low","Minor","N/A"),
    (4,"Aleksandra Pujanek","A board with name of + could not be created","Create a board with given name: +","Response Code:200 - OK, Board is created with name: +","Response Code:400 - Bad Request","2023-10-27 10:36:47","Low","Minor","N/A");
```
Output:

![16-response4](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/16-response4.png?raw=true)
![16-response3](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/16-response3.png?raw=true)

---

17. Add to the 'Defects' table column for Risk Assessment (Priority x Severity).
    
```sql
ALTER TABLE Defects
  ADD Risk_Assessment INTEGER
    DEFAULT "";
```
Output:

![17-response](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/17-response.png?raw=true)

---

18. Remove from 'Defects' table column for BA assessment.
    
```sql
ALTER TABLE Defects
  DROP  BA_Assessment;
```
Output:

*Unavailable to perform and present - the user in [free w3schools SQL editor](https://www.w3schools.com/sql/trysql.asp?filename=trysql_editor) is not allowed to delete columns from database*

---

19. Rename  'Defects' table to 'Defects_phase1'.
    
```sql
ALTER TABLE Defects
  RENAME TO Defects_phase1;
```
Output:

![19-response](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/19-response.png?raw=true)

---

20. Delete  'Defects_phase1' table.
    
```sql
DROP TABLE IF EXISTS Defects_phase1;
```

Output:

![20-response](https://github.com/AleksandraPujanek/SQLrequests/blob/main/images/20-response.png?raw=true)
