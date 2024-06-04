# mySQLTest
+--------------------------+---------+-------------+------------+--------+
| Title                    | Runtime | Genre       | IMDB_Score | Rating |
+--------------------------+---------+-------------+------------+--------+
| Howard the Duck          |     110 | Sci-Fi      |        4.6 | PG     |
| Lavalantula              |      83 | Horror      |        4.7 | TV-14  |
| Starship Troopers        |     129 | Sci-Fi      |        7.2 | R      |
| Waltz With Bashir        |      90 | Documentary |        8.0 | R      |
| Spaceballs               |      96 | Comedy      |        7.1 | PG     |
| Monsters Inc.            |      92 | Animation   |        8.1 | G      |
| The Shawshank Redemption |     142 | Drama       |        9.3 | R      |
| The Godfather            |     177 | Crime       |        9.2 | R      |
+--------------------------+---------+-------------+------------+--------+
Add two more movies of your choosing to the table. - 
    INSERT INTO Movies (Title, Runtime, Genre, IMDB_Score, Rating)
    -> VALUES ('The Shawshank Redemption', '142', 'Drama', '9.3', 'R'),
    ->        ('The Godfather', '177', 'Crime', '9.2', 'R');

Create a query to find all movies in the Sci-Fi genre. - 
 SELECT *
    -> FROM Movies
    -> WHERE Genre = 'Sci-Fi';
+-------------------+---------+--------+------------+--------+
| Title             | Runtime | Genre  | IMDB_Score | Rating |
+-------------------+---------+--------+------------+--------+
| Howard the Duck   |     110 | Sci-Fi |        4.6 | PG     |
| Starship Troopers |     129 | Sci-Fi |        7.2 | PG-13  |
+-------------------+---------+--------+------------+--------+

Create a query to find all films that scored at least a 6.5 on IMDB - 
 SELECT *
    -> FROM Movies
    -> WHERE IMDB_Score >= 6.5;
+--------------------------+---------+-------------+------------+--------+
| Title                    | Runtime | Genre       | IMDB_Score | Rating |
+--------------------------+---------+-------------+------------+--------+
| Starship Troopers        |     129 | Sci-Fi      |        7.2 | PG-13  |
| Waltz With Bashir        |      90 | Documentary |        8.0 | R      |
| Spaceballs               |      96 | Comedy      |        7.1 | PG     |
| Monsters Inc.            |      92 | Animation   |        8.1 | G      |
| The Shawshank Redemption |     142 | Drama       |        9.3 | R      |
| The Godfather            |     177 | Crime       |        9.2 | R      |
+--------------------------+---------+-------------+------------+--------+

For parents who have young kids, but who don't want to sit through long children's movies, create a query to find all of the movies rated G or PG that are less than 100 minutes long. - 
SELECT *
    -> FROM Movies
    -> WHERE Rating = 'G' OR Rating = 'PG' AND Runtime < 100;
+---------------+---------+-----------+------------+--------+
| Title         | Runtime | Genre     | IMDB_Score | Rating |
+---------------+---------+-----------+------------+--------+
| Spaceballs    |      96 | Comedy    |        7.1 | PG     |
| Monsters Inc. |      92 | Animation |        8.1 | G      |
+---------------+---------+-----------+------------+--------+
    
Create a query to show the average runtimes of movies scoring below a 7.5 on imdb, grouped by their respective genres. - 
SELECT Genre, AVG(Runtime) AS Average_Runtime
    -> FROM Movies
    -> WHERE IMDB_Score < 7.5
    -> GROUP BY Genre;
+--------+-----------------+
| Genre  | Average_Runtime |
+--------+-----------------+
| Sci-Fi |        119.5000 |
| Horror |         83.0000 |
| Comedy |         96.0000 |
+--------+-----------------+


There's been a data entry mistake; Starship Troopers is actually rated R, not PG-13. Create a query that finds the movie by its title and changes its rating to R. - 
UPDATE movies 
    -> SET Rating = 'R'
    -> WHERE title = 'Starship Troopers';
+--------------------------+---------+-------------+------------+--------+
| Title                    | Runtime | Genre       | IMDB_Score | Rating |
+--------------------------+---------+-------------+------------+--------+
| Howard the Duck          |     110 | Sci-Fi      |        4.6 | PG     |
| Lavalantula              |      83 | Horror      |        4.7 | TV-14  |
| Starship Troopers        |     129 | Sci-Fi      |        7.2 | R      |
| Waltz With Bashir        |      90 | Documentary |        8.0 | R      |
| Spaceballs               |      96 | Comedy      |        7.1 | PG     |
| Monsters Inc.            |      92 | Animation   |        8.1 | G      |
| The Shawshank Redemption |     142 | Drama       |        9.3 | R      |
| The Godfather            |     177 | Crime       |        9.2 | R      |
+--------------------------+---------+-------------+------------+--------+


Show the ID number and rating of all of the Horror and Documentary movies in the database. Do this in only one query or two queries. - 
SELECT Title, Rating
    -> FROM Movies
    -> WHERE Genre = 'Horror' or Genre = 'Documentary';
+-------------------+--------+
| Title             | Rating |
+-------------------+--------+
| Lavalantula       | TV-14  |
| Waltz With Bashir | R      |
+-------------------+--------+
This time let's find the average, maximum, and minimum IMDB score for movies of each rating. - 
SELECT Rating, 
    -> AVG(IMDB_Score) AS Average_Score, 
    -> MAX(IMDB_Score) AS Highest_Score, 
    -> MIN(IMDB_Score) AS Lowest_Score
    -> FROM Movies
    -> GROUP BY Rating;
+--------+---------------+---------------+--------------+
| Rating | Average_Score | Highest_Score | Lowest_Score |
+--------+---------------+---------------+--------------+
| PG     |       5.85000 |           7.1 |          4.6 |
| TV-14  |       4.70000 |           4.7 |          4.7 |
| R      |       8.42500 |           9.3 |          7.2 |
| G      |       8.10000 |           8.1 |          8.1 |
+--------+---------------+---------------+--------------+

Use a HAVING COUNT(*) > 1 clause to only show ratings with multiple movies showing. -
SELECT Rating, 
    -> AVG(IMDB_Score) AS Average_Score, 
    -> MAX(IMDB_Score) AS Highest_Score, 
    -> MIN(IMDB_Score) AS Lowest_Score
    -> FROM Movies
    -> GROUP BY Rating
    -> HAVING COUNT(*) > 1;
+--------+---------------+---------------+--------------+
| Rating | Average_Score | Highest_Score | Lowest_Score |
+--------+---------------+---------------+--------------+
| PG     |       5.85000 |           7.1 |          4.6 |
| R      |       8.42500 |           9.3 |          7.2 |
+--------+---------------+---------------+--------------+

Make the movie list more child-friendly. Delete all entries that have a rating of R. - 
DELETE FROM movies 
    -> WHERE Rating = 'R';

+-----------------+---------+-----------+------------+--------+
| Title           | Runtime | Genre     | IMDB_Score | Rating |
+-----------------+---------+-----------+------------+--------+
| Howard the Duck |     110 | Sci-Fi    |        4.6 | PG     |
| Lavalantula     |      83 | Horror    |        4.7 | TV-14  |
| Spaceballs      |      96 | Comedy    |        7.1 | PG     |
| Monsters Inc.   |      92 | Animation |        8.1 | G      |
+-----------------+---------+-----------+------------+--------+


    






