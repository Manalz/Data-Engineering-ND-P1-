This project uses Postgres SQL quries to analyze the data of a startup called Sparkify which they've been collecting on songs and user activity on their new music streaming app. Thier data resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app. The project goal is to create a Postgres database with tables designed to optimize queries on song play analysis by creating a database schema and ETL pipeline for this analysis and test the created database and ETL pipeline by running queries given by the analytics team from Sparkify and compare the results with their expected results.

The project repository contains the following files:

1. 'sql_queries.py' that contains all DROPs, CREATEs, and INSERTs SQL quiries. 
2. 'create_tables.py' is a python lines of code, which can be run to reset the tables before each time running       ETL pipelines.
3. 'etl.ipynb' that fetches and processes the data given by data set from song_data and log_data. It also             contains the instructions on the ETL process for all tables in the database.
4. 'etl.py' to read and process files from song_data and log_data and loads them into the tables. This can be         filled out based on your work in the ETL notebook.
5. 'test.ipynb' to check the validity of creating and inserting the tables in the database.


The song and log datasets will be used for the project database. A star schema is chosen to be optimized for queries on song play analysis. This includes the following tables:

Fact Table:
    - songplays - records in log data associated with song plays i.e. records with page NextSong
      songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent
Dimension Tables:
   - users - users in the app
      user_id, first_name, last_name, gender, level
   - songs - songs in music database
      song_id, title, artist_id, year, duration
   - artists - artists in music database
       artist_id, name, location, latitude, longitude
   - time - timestamps of records in songplays broken down into specific units
       start_time, hour, day, week, month, year, weekday
       
The ETL processes includes the following steps respectively:
- Process song_data by fetching and read the first song file from the list of song JSON files in data/song_data.
- Select the appropriate values from that file for the songs table's column.
- Insert the selected values into songs table.
- Select the appropriate values from that selected song file for the artists table's column.
- Insert the selected values into artists table.
- Process log_data by fetching and read the first log file from the list of log JSON files in data/log_data.
- Extract the data for time table by filtering the records by 'NextSong', converting the `ts` timestamp column to   datetime, and getting the timestamp, hour, day, week of year, month, year, and weekday from the `ts` column       given by that selected log file.
- Insert the obtained values into time table.
- Select the appropriate values from that log file for the users table's column.
- Insert the selected values into users table.
- Finally, insert the appropriate songplay records into songplay table.
       
       
To run the project, you should do the following steps:

 1. run create_tables.py in Terminal using the command 'python create_tables.py'. You can check the validity of       creating tables by running cells in 'test.ipynb' 
 2. run all cells in 'etl.ipynb'. You can check the validity of inserting data into the tables by running cells in 'test.ipynb' 
 3. run etl.py in Terminal using the command 'python etl.py'
 
 