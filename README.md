# PostgreSQL_psycopg2_SQLAlchemy_project
## Overview and Summary:
There are 6 Jupyter Python notebooks uploaded onto this repository. The scripts/Jupyter notebooks can be found in the 2 folders, which contain 2+ notebooks using the psyocpg2 and SQLAlchemy libraries, respectively. Here's a brief synopsis of what these folders contain:

a.) psycopg2: contains 3 Jupyter notebook files (Parts I, V, and VI) of Python code implementing commands on a PostgreSQL database via the psycopg2 library. Part VI uses the IMDB dataset curated and extracted via an ETL and web crawler program from one of my other GitHub repos.

b.) SQLAlchemy: contains 3 Jupyter notebook files (Parts II through IV) of Python code implementing commands on a PostgreSQL database via the SQLAlchemy library. This inclues importing a CSV file and inserting the data into a new SQL table, creating a table and inserting data manually, and implementing various SELECT queries.


For this repository, I used a PostGreSQL server to implement part of the CRUD process (i.e., create a table within a database, insert records/rows of data into 1 or more of the table's columns, update records of data, and delete data) and some SELECT queries. 

## Code samples:
Before describing the project in more detail, here are a few code samples from the project:

The following code uses the pandas library to import data from a Pandas Dataframe into a PostgreSQL database:
```
#import SQLAlchemy engine for connecting to a postgreSQL database
from sqlalchemy import create_engine

#initialize SQLAlchemy engine by specifying login details and name of database
eng = create_engine("postgres://postgres:********@localhost:5433/films")

#use to_sql() method to export the imdb_metascore dataframe to the SQL database as a table
imdb_data.to_sql("imdb_data", eng)
```

The following code implements a SELECT...WHERE query using the psycopg2 library. The following query selects data from the IMDB dataset in which the film genre comprises Film-Noir (e.g., Double Indemnity):
```
import psycopg2 

connection = None

try:
    #specify database, username, password, etc. so Python can connect to it via the psycopg2 library
    connection = psycopg2.connect(database="films", user = "postgres", password = "*******", host="localhost", port="5433")
    #initialize connection to database
    cursor = connection.cursor()
    
    #specify and execute SELECT query
    
    cursor.execute("""SELECT name, year, imdb_rating, length FROM imdb_data WHERE genre ='Film-Noir';""")
    
    results = cursor.fetchall()
    
    for res in results:
        #print out the SELECT query output
        print(res)
        
except psycopg2.DatabaseError:
    if connection:
        #i.e., if an error occurs, do NOT commit any change to database
        connection.rollback()

#except when an error occurs, commit the changes to the database
connection.commit

#having implemented the query, close off the connection to the database
connection.close()
cursor.close()
```
## More detailed synopsis of repo:
In one of these files (refer to the "SQLAlchemy" folder, and open the "Part_II..." *.ipny notebook file), I also implement some more advanced queries, such as JOIN commands: FULL OUTER JOINs and an INNER JOIN. 

To implement these SQL commands, I used 2 different Python libraries.First, I used the psycopg2 library, which allows one to implement SQL code as strings embedded within a try...except loop of Python code. Second, I used SQLalchemy to implement more Pythonic code to implement similar SQL commands, but using a different dataset for extra contrast. For Part II, I merely insert data in manually using the equivalent of an "INSERT INTO" command. 

However, for Part III, instead of merely inserting data bia "INSERT INTO, this notebook and code imports a CSV file, with some IGN video and PC game ratings data, into a new table within a PostgreSQL database. 

1.) For Part I of the uploaded Jupyter notebooks, the data used to create and insert data into the database comprises employment and other economic data on several software and biotech companies based in the SF Bay Area. The CRUD and SELECT queries implemented on these data makes use of the psycopg2 library.

2.) For the Jupyter notebooks of Part II through IV, I used gamefaqs and IGN video game ratings data. I imported the SQLAlchemy library to implement various SQL commands on a PostgreSQL server and database. However, as noted above, the syntax is different and much more similar to regular Python code. In addition, SQLAlchemy allows for SQL commands to be implemented more efficiently than psycopg2. 

3.) Part V implements some more advanced SELECT queries, such as: 
a.) aggregation methods (e.g, AVG, COUNT, SUM);
b.) SELECT...WHERE...LIKE to query on specific string charactersitics (e.g., company names starting with "S"); 
c.) clauses for modifying or rerranging aggregates, such as GROUP BY, ORDER BY, and HAVING; 
d.) various boolean operators such as BETWEEN (i.e., for specifying ranges) and OR. 

4.) Part VI takes the IMDB films data--the same datasets as those I created via the web crawler in the "Python_Web_Crawler_IMDB_data_analysis" repo--and creates a new table within a PostgreSQL database, inserting the IMDB films data into this table. The notebook then proceeds to perform various queries on the data, especially those pertaining to film genre and IMDB ratings.

### Packages required to run these scripts:

/* The various Python script were run using Python 3.7 via Jupyter notebooks. Several data analysis and data visualization libraries
are used in these scripts, in addition to beautifulsoup, which was used to implement part of the web crawler apps.

Here's a complete list of the libraries that are used (excluding some of the specific modules contained within these libraries):

matlotlib; Pandas; Seaborn; StatsModels; numpy; BeautifulSoup; requests; time; random; warnings; SQLAlchemy; and psycopg2.


Anaconda and Jupyter is not necessarily needed for implementing the scripts, but would be recommended since Anaconda
contains many of these libraries built into them--e.g., Pandas, matplotlib. 

If using Anaconda/Jupyter, only 1 additional library--the beautifulsoup library-- will be required to install separately, 
via pip install on terminal:
<<< pip install beautifulsoup4

### Caveats: 
The database does not contain any sensitive information, but the actual username and password to the database have been replaced with a fake username and password (to help avoid SQL injections) after the cells in the Jupyter notebook were already implemented.  
