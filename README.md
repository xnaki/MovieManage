-- Database Schema
CREATE TABLE Movies (
    movie_id INT PRIMARY KEY,
    title VARCHAR(100) NOT NULL,
    genre VARCHAR(50),
    release_year INT,
    director VARCHAR(100),
    actors VARCHAR(255),
    rating DECIMAL(3, 1),
    personal_review TEXT,
    date_viewed DATE
);

CREATE TABLE CustomLists (
    list_id INT PRIMARY KEY,
    list_name VARCHAR(50) NOT NULL
);

CREATE TABLE MovieLists (
    movie_id INT,
    list_id INT,
    FOREIGN KEY (movie_id) REFERENCES Movies(movie_id),
    FOREIGN KEY (list_id) REFERENCES CustomLists(list_id),
    PRIMARY KEY (movie_id, list_id)
);

-- Inserting Movies
INSERT INTO Movies (movie_id, title, genre, release_year, director, actors, rating, personal_review, date_viewed)
VALUES 
    (1, 'Movie 1', 'Action', 2010, 'Director A', 'Actor1, Actor2, Actor3', 8.5, 'Great movie!', '2023-01-15'),
    (2, 'Movie 2', 'Comedy', 2015, 'Director B', 'Actor4, Actor5', 7.9, 'Funny and entertaining', '2023-02-20')
    -- Add more movies as needed
    ;

-- Searching and Filtering Movies
SELECT * FROM Movies WHERE genre = 'Action';
SELECT * FROM Movies WHERE director = 'Director A';
SELECT * FROM Movies WHERE actors LIKE '%Actor1%' OR actors LIKE '%Actor2%';
SELECT * FROM Movies WHERE rating >= 8.0;
SELECT * FROM Movies WHERE date_viewed BETWEEN '2023-01-01' AND '2023-12-31';

-- Creating Custom Lists
INSERT INTO CustomLists (list_id, list_name) VALUES (1, 'Favorites'), (2, 'Watched'), (3, 'To-Watch');

-- Adding movies to custom lists (e.g., adding Movie 1 to Favorites)
INSERT INTO MovieLists (movie_id, list_id) VALUES (1, 1);

-- Retrieving Movies from Custom Lists (e.g., Favorites)
SELECT Movies.* FROM Movies
INNER JOIN MovieLists ON Movies.movie_id = MovieLists.movie_id
WHERE MovieLists.list_id = 1;
