To list available databases:

show databases;

The general command for creating a database:

CREATE DATABASE <database_name>;

A specific example:

CREATE DATABASE soap_store;

To drop a database:

DROP DATABASE <database-name>;

To use a database:

USE <database-name>; 

Creating Tables:

    CREATE TABLE cats (
        name VARCHAR(50),
        age INT
    );
     
    CREATE TABLE dogs (
        name VARCHAR(50),
        breed VARCHAR(50),
        age INT
    );

SHOW tables;


SHOW COLUMNS FROM cats;


DESC cats; 

To drop a table:

DROP TABLE <table-name>;

To specifically drop the cats table:

DROP TABLE cats; 

Insert Basics

    CREATE TABLE cats (
        name VARCHAR(50),
        age INT
    );


Insert a cat:

    INSERT INTO cats (name, age) 
    VALUES ('Blue Steele', 5);

And another:

    INSERT INTO cats (name, age) 
    VALUES ('Jenkins', 7);

To view all rows in our table:

SELECT * FROM cats; 

-- Single insert (switching order of name and age)

    INSERT INTO cats (age, name) 
    VALUES 
      (2, 'Beth');


-- Multiple Insert:

    INSERT INTO cats (name, age) 
    VALUES 
      ('Meatball', 5), 
      ('Turkey', 1), 
      ('Potato Face', 15);

Using NOT NULL:

    CREATE TABLE cats2 (
        name VARCHAR(100) NOT NULL,
        age INT NOT NULL
    );

Define a table with a DEFAULT name specified:

    CREATE TABLE cats3  (    
        name VARCHAR(20) DEFAULT 'no name provided',    
        age INT DEFAULT 99  
    );

Notice the change when you describe the table:

DESC cats3;

Insert a cat without a name:

INSERT INTO cats3(age) VALUES(13);

Or a nameless, ageless cat:

INSERT INTO cats3() VALUES();

Combine NOT NULL and DEFAULT:

    CREATE TABLE cats4  (    
        name VARCHAR(20) NOT NULL DEFAULT 'unnamed',    
        age INT NOT NULL DEFAULT 99 
    );

-- One way of specifying a PRIMARY KEY

    CREATE TABLE unique_cats (
    	cat_id INT PRIMARY KEY,
        name VARCHAR(100) NOT NULL,
        age INT NOT NULL
    );


-- Another option:


    CREATE TABLE unique_cats2 (
    	cat_id INT,
        name VARCHAR(100) NOT NULL,
        age INT NOT NULL,
        PRIMARY KEY (cat_id)
    );

--  AUTO_INCREMENT


    CREATE TABLE unique_cats3 (
        cat_id INT AUTO_INCREMENT,
        name VARCHAR(100) NOT NULL,
        age INT NOT NULL,
        PRIMARY KEY (cat_id)
    );

-- To get all the columns:

SELECT * FROM cats;


-- To only get the age column:

SELECT age FROM cats;


-- To select multiple specific columns:

SELECT name, breed FROM cats; 

-- Use where to specify a condition:

SELECT * FROM cats WHERE age = 4;

       

SELECT * FROM cats WHERE name ='Egg'; 

-- Use 'AS' to alias a column in your results (it doesn't actually change the name of the column in the table)

SELECT cat_id AS id, name FROM cats; 

CODE: Updating Data

Change tabby cats to shorthair:

UPDATE cats SET breed='Shorthair' WHERE breed='Tabby';

Another update:

UPDATE cats SET age=14 WHERE name='Misty';

-- Delete all cats with name of 'Egg':

DELETE FROM cats WHERE name='Egg';

-- Delete all rows in the cats table:

DELETE FROM cats; 

Concatenate strings:

    SELECT CONCAT('pi', 'ckle');
     
    SELECT CONCAT(author_fname,' ', author_lname) AS author_name FROM books;
     
    SELECT CONCAT_WS('-',title, author_fname, author_lname) FROM books;

Use SUBSTR to select parts of a string:

    SELECT SUBSTRING('Hello World', 1, 4);
     
    SELECT SUBSTRING('Hello World', 7);
     
    SELECT SUBSTRING('Hello World', -3);
     
    SELECT SUBSTRING(title, 1, 10) AS 'short title' FROM books;
     
    SELECT SUBSTR(title, 1, 10) AS 'short title' FROM books;

Combine string functions:

    SELECT CONCAT
        (
            SUBSTRING(title, 1, 10),
            '...'
        ) AS 'short title'
    FROM books;

Replace parts of a string:

    SELECT REPLACE('Hello World', 'Hell', '%$#@');
     
    SELECT REPLACE('Hello World', 'l', '7');
     
    SELECT REPLACE('Hello World', 'o', '0');
     
    SELECT REPLACE('HellO World', 'o', '*');
     
    SELECT
      REPLACE('cheese bread coffee milk', ' ', ' and ');
     
    SELECT REPLACE(title, 'e ', '3') FROM books;
     
    SELECT REPLACE(title, ' ', '-') FROM books;

Reverse the order of a string of chars:

    SELECT REVERSE('Hello World');
     
    SELECT REVERSE('meow meow');
     
    SELECT REVERSE(author_fname) FROM books;
     
    SELECT CONCAT('woof', REVERSE('woof'));
     
    SELECT CONCAT(author_fname, REVERSE(author_fname)) FROM books;

Get the lenght in chars of a string:

    SELECT CHAR_LENGTH('Hello World');
     
    SELECT CHAR_LENGTH(title) as length, title FROM books;
     
    SELECT author_lname, CHAR_LENGTH(author_lname) AS 'length' FROM books;
     
    SELECT CONCAT(author_lname, ' is ', CHAR_LENGTH(author_lname), ' characters long') FROM books;

Capitalize or minusculize 

    SELECT UPPER('Hello World');
     
    SELECT LOWER('Hello World');
     
    SELECT UPPER(title) FROM books;
     
    SELECT CONCAT('MY FAVORITE BOOK IS ', UPPER(title)) FROM books;
     
    SELECT CONCAT('MY FAVORITE BOOK IS ', LOWER(title)) FROM books;


Some additional functions:

    SELECT INSERT('Hello Bobby', 6, 0, 'There'); 
     
    SELECT LEFT('omghahalol!', 3);
     
    SELECT RIGHT('omghahalol!', 4);
     
    SELECT REPEAT('ha', 4);
     
    SELECT TRIM('  pickle  ');

Selections:

DISTINCT functions allows to select unique values from a table.

    SELECT author_lname FROM books;
     
    SELECT DISTINCT author_lname FROM books;
     
    SELECT author_fname, author_lname FROM books;
     
    SELECT DISTINCT CONCAT(author_fname,' ', author_lname) FROM books;
     
    SELECT DISTINCT author_fname, author_lname FROM books;

ORDER BY: 

    SELECT * FROM books
    ORDER BY author_lname;
     
    SELECT * FROM books
    ORDER BY author_lname DESC;
     
    SELECT * FROM books
    ORDER BY released_year;

    ALSO:

        SELECT book_id, author_fname, author_lname, pages
    FROM books ORDER BY 2 desc;
     
    SELECT book_id, author_fname, author_lname, pages
    FROM books ORDER BY author_lname, author_fname;

LIMIT:

    SELECT title FROM books LIMIT 3;
     
    SELECT title FROM books LIMIT 1;
     
    SELECT title FROM books LIMIT 10;
     
    SELECT * FROM books LIMIT 1;
     
    SELECT title, released_year FROM books 
    ORDER BY released_year DESC LIMIT 5;
     
    SELECT title, released_year FROM books 
    ORDER BY released_year DESC LIMIT 1;
     
    SELECT title, released_year FROM books 
    ORDER BY released_year DESC LIMIT 14;
     
    SELECT title, released_year FROM books 
    ORDER BY released_year DESC LIMIT 0,5;
     
    SELECT title, released_year FROM books 
    ORDER BY released_year DESC LIMIT 0,3;
     
    SELECT title, released_year FROM books 
    ORDER BY released_year DESC LIMIT 1,3;
     
    SELECT title, released_year FROM books 
    ORDER BY released_year DESC LIMIT 10,1;
     
    SELECT * FROM tbl LIMIT 95,18446744073709551615;
     
    SELECT title FROM books LIMIT 5;
     
    SELECT title FROM books LIMIT 5, 123219476457;
     
    SELECT title FROM books LIMIT 5, 50;

LIKE: 

    SELECT title, author_fname, author_lname, pages 
    FROM books
    WHERE author_fname LIKE '%da%'; Finds anything that contains da
     
    SELECT title, author_fname, author_lname, pages 
    FROM books
    WHERE title LIKE '%:%'; 
     
    SELECT * FROM books
    WHERE author_fname LIKE '____'; With the underscore, it finds any string that has the same amount of underscores you enter
     
    SELECT * FROM books
    WHERE author_fname LIKE '_a_'; Finds everything that has a char, the letter a (in this case) and another char.

    To escape % and _
        -- To select books with '%' in their title:
        SELECT * FROM books
        WHERE title LIKE '%\%%';
        
        -- To select books with an underscore '_' in title:
        SELECT * FROM books
        WHERE title LIKE '%\_%';