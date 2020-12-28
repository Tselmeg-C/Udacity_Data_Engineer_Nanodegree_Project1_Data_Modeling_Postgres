# Project: Data Modeling with Postgres

## 1.Project Description

This is the first project of the Udacity Data Engineer Nanodegree. The task is to create a database with tables designed to optimize queries on song play analysis for a fictionary music streaming service provider, who is interested in understanding what songs users are listening to. The data collected on user activity and songs are resideing separately in a directory of JSON logs on user activity and a directory with JSON metadata on the songs in their app. 

A Postgres database schema and ETL pipeline are created for this analysis purpose. I have defined fact and dimension tables for a star schema, and designed an ETL pipeline that transfers data from files in two local directories into these tables in Postgres using Python and SQL. 

## 2.The Dataset

### 2.1 Song Dataset
The first dataset is a subset of real data from the [Million Song Dataset](http://millionsongdataset.com/). Each file is in JSON format and contains metadata about a song and the artist of that song. The files are partitioned by the first three letters of each song's track ID. For example, here are filepaths to two files in this dataset.

>song_data/A/B/C/TRABCEI128F424C983.json

>song_data/A/A/B/TRAABJL12903CDCF1A.json

And below is an example of what a single song file, TRAABJL12903CDCF1A.json, looks like.

>{"num_songs": 1, "artist_id": "ARJIE2Y1187B994AB7", "artist_latitude": null, "artist_longitude": null, "artist_location": "", "artist_name": "Line Renaud", "song_id": "SOUPIRU12A6D4FA1E1", "title": "Der Kleine Dompfaff", "duration": 152.92036, "year": 0}

### 2.2 Log Dataset

The second dataset consists of log files in JSON format generated by this event simulator based on the songs in the dataset above. These simulate activity logs from a music streaming app based on specified configurations.

The log files in the dataset are partitioned by year and month. For example, here are filepaths to two files in this dataset.

>log_data/2018/11/2018-11-12-events.json

>log_data/2018/11/2018-11-13-events.json

And below is an example of what the data in a log file, 2018-11-12-events.json, looks like.
![alt text](https://github.com/Tselmeg-C/Udacity_Data_Engineer_Nanodegree_Project1_Data_Modeling_Postgres/blob/main/log-data.png)

## 3.Schema for Song Play Analysis

A star schema was designed. This includes the following tables.

__Fact Table__

__1.songplays__ - records in log data associated with song plays i.e. records with page NextSong

* songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent

__Dimension Tables__

__2.users__ - users in the app

* user_id, first_name, last_name, gender, level

__3.songs__ - songs in music database

* song_id, title, artist_id, year, duration

__4.artists__ - artists in music database

* artist_id, name, location, latitude, longitude

__5.time__ - timestamps of records in songplays broken down into specific units

* start_time, hour, day, week, month, year, weekday

## 4.Project Files

__test.ipynb__ displays the first few rows of each table to let you check your database.

__create_tables.py__ drops and creates the tables. This should be run to reset the tables before each time the ETL scripts are run.

__etl.ipynb__ reads and processes a single file from song_data and log_data and loads the data into the tables. This notebook contains detailed instructions on the ETL process for each of the tables.

__etl.py__ reads and processes files from song_data and log_data and loads them into the tables. 

__sql_queries.py__ contains all the sql queries, and is imported into the last three files above.

__README.md__ provides information of this project.

## 5.How to run the Python scripts

* Run __create_tables.py__ to create the sparkifydb database, and the five tables. 
* Run __etl.py__ to insert records into the tables. 
* Run __test.ipynb__, __etl.ipynb__, or __etl.py__ successfully only after running __create_tables.py__ at least once.
* When rerunning __test.ipynb__ remember to restart this notebook to close the connection to the database. Otherwise, it won't be able to run the code in __create_tables.py__, __etl.py__, or __etl.ipynb__ files since multiple connections to the same database is not possible.