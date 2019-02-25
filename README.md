# PostgreSQL_psycopg2_SQLAlchemy_project

For this repository, I used a PostGreSQL server to implement part of the CRUD process (i.e., create a table within a database, insert rows of data into 1 or more of the table's columns, update rows of data, and delete data) and some SELECT queries. In one of these files (see the "Using SQLAlchemy..." ipython notebook file), I also implement some more advanced queries, such as JOIN commands: FULL OUTER JOINs and an INNER JOIN. 

To implement these SQL commands, I used 2 different Python libraries.First, I used the psycopg2 library, which allows one to implement SQL code as strings embedded within a try...except loop of Python code. Second, I used SQLalchemy to implement more Pythonic code to implement similar SQL commands, but using a different dataset for extra contrast.Instead of merely inserting data, this code imports a CSV file with some gaming data. 

1.) For 1 of the uploaded Jupyter notebooks, the data used to create and insert data into the database comprises employment and other economic data on several software and biotech companies based in the SF Bay Area. The CRUD and SELECT queries implemented on these data makes use of the psycopg2 library.

2.) For the other notebook, I used gamefaqs and IGN video game ratings data, and used SQLAlchemy to implement similar SQL commands to the same PostGreSQL server. However, as noted above, the syntax is different and much more similar to regular Python code. In addition, SQLAlchemy allows for SQL commands to be implemented more efficiently than psycopg2. 

Caveats: 
The database does not contain any sensitive information, so the password and database information are shown. Of course, this would not be implemented if I was doing a project for a company's personal database or any database containing sensitive and/or confidential data. 
