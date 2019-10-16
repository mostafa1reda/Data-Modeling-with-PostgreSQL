# Sparkify Postgres ETL

This is the first project submission for the Data Engineering Nanodegree.

This project consists of putting into practice the following concepts:
- Data modeling with Postgres
- Database star schema created 
- ETL pipeline using Python

## Project Summary

The objective of this project is to create a SQL analytics database for a fictional music streaming service called Sparkify. Sparkify's analytics team seeks to understand what, when and how users are playing songs on the company's music app. The analysts need an easy way to query and analyze the data, which is currently locally stored in raw JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app on.

As the data engineer assigned to the project, My role is to create a database schema and upload the data into a PostgreSQL database and implement an ETL pipeline for this analysis.

### Data

- **Song datasets**: all json files are nested in subdirectories under */data/song_data*. A sample of this files is:

```
{"num_songs": 1, "artist_id": "ARJIE2Y1187B994AB7", "artist_latitude": null, "artist_longitude": null, "artist_location": "", "artist_name": "Line Renaud", "song_id": "SOUPIRU12A6D4FA1E1", "title": "Der Kleine Dompfaff", "duration": 152.92036, "year": 0}
```

- **Log datasets**: all json files are nested in subdirectories under */data/log_data*. A sample of a single row of each files is:

```
{"artist":"Slipknot","auth":"Logged In","firstName":"Aiden","gender":"M","itemInSession":0,"lastName":"Ramirez","length":192.57424,"level":"paid","location":"New York-Newark-Jersey City, NY-NJ-PA","method":"PUT","page":"NextSong","registration":1540283578796.0,"sessionId":19,"song":"Opium Of The People (Album Version)","status":200,"ts":1541639510796,"userAgent":"\"Mozilla\/5.0 (Windows NT 6.1) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/36.0.1985.143 Safari\/537.36\"","userId":"20"}
```
## Database Schema

The schema used for this exercise is the Star Schema: 
There is one main fact table containing all the measures associated with each event *songplays*, 
and 4-dimensional tables *songs*, *artists*, *users* and *time*, each with a primary key that is being referenced from the fact table.

On why to use a relational database for this case:

- The data types are structured (we know before-hand the structure of the jsons we need to analyze, and where and how to extract and transform each field)
- The amount of data we need to analyze is not big enough to require big data related solutions.
- This structure will enable the analysts to aggregate the data efficiently
- Ability to use SQL that is more than enough for this kind of analysis
- We need to use JOINS for this scenario

## Project structure

Files used on the project:
1. **data** folder nested at the home of the project, where all needed jsons reside.
2. **sql_queries.py** contains all your SQL queries, and is imported into the files bellow.
3. **create_tables.py** drops and creates tables. You run this file to reset your tables before each time you run your ETL scripts.
4. **test.ipynb** displays the first few rows of each table to let you check your database.
5. **etl.ipynb** reads and processes a single file from song_data and log_data and loads the data into your tables. 
6. **etl.py** reads and processes files from song_data and log_data and loads them into your tables. 
7. **README.md** current file, provides discussion on my project.

## Data Processing and Quality Checks

Data is extracted from two types of JSON source files: song data from the [Million Song Dataset](https://labrosa.ee.columbia.edu/millionsong/) and songplay data from user logs. The JSON files are read into pandas dataframes, processed and uploaded into the database using psycopg2. 

A number of steps clean the data and reduce the size of the database by removing data not needed for the analysis: 
* Songplays are identified by filtering for actions initiated from the 'NextSong' page. 
* Timestamps are converted from UNIX time to datetime format.

## How to Use

1. Run create_tables.py from terminal to set up the database and tables.
2. Run etl.py from terminal to process and load data into the database.
3. Launch test.ipynb to run validation and example queries.

## Author 
Mostafa Reda (https://www.linkedin.com/in/mostafaali96/)
