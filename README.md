# SQLrequests
Repo with helpful SQL requests.

1. Find the movies not released in the years between 2000 and 2010 (from Movie table)

![1-base-table](https://raw.githubusercontent.com/AleksandraPujanek/SQLrequests/main/images/1-base-table.png)

Solution no 1
```sql
SELECT title, year FROM movies
WHERE year < 2000 OR year > 2010;
```

Solution no 2
```sql
SELECT Title, year FROM Movies
WHERE Year NOT BETWEEN 2000 AND 2010;
```
Output:<br>
![1-response](https://raw.githubusercontent.com/AleksandraPujanek/SQLrequests/main/images/1-response.png)
2. 
