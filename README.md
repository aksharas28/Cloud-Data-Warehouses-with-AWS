Building a Data Warehouse ETL pipeline for Sparkify:

Introduction:

Spariky provides music streaming data to its users. The songs details and the user activity details are collected and stored in the form of JSON. This project helps spariky to make adhoc queries against their data using data warehousing concepts.

Description:

Sparkify is a facing lot of problems querying its own data stored in json. They require to query and do lots of analytics and also their analytics drive their data science team as well. So, inorder to make things easy for them we are building an etl pipeline here which consumer json data store in s3 and store them as staging tables in redshift and later on creating facts and dimension tables out of the staging tables and inserting data. Facts and dimensional tables reside in redshift which uses columnar storage which increases our querying capability providing quick results.

Datasets:

Log Dataset:

{"artist":"Pavement", "auth":"Logged In", "firstName":"Sylvie", "gender", "F", "itemInSession":0, "lastName":"Cruz", "length":99.16036, "level":"free", "location":"Klamath Falls, OR", "method":"PUT", "page":"NextSong", "registration":"1.541078e+12", "sessionId":345, "song":"Mercy:The Laundromat", "status":200, "ts":1541990258796, "userAgent":"Mozilla/5.0(Macintosh; Intel Mac OS X 10_9_4...)", "userId":10}

Song Dataset:

{"num_songs": 1, "artist_id": "ARJIE2Y1187B994AB7", "artist_latitude": null, "artist_longitude": null, "artist_location": "", "artist_name": "Line Renaud", "song_id": "SOUPIRU12A6D4FA1E1", "title": "Der Kleine Dompfaff", "duration": 152.92036, "year": 0}

Schema for fact table and dimensional tables:

fact table - songplays:

songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent

Dimensional tables - users, songs, artists, time:

users - user_id, first_name, last_name, gender, level songs - song_id, title, artist_id, year, duration artists - artist_id, name, location, latitude, longitude time - start_time, hour, day, week, month, year, weekday

Schema for staging tables - stagingevents, stagingsongs:

stagingevents - event_id, artist, auth, firstName, gender, itemInSession, lastName, length, level, location, method, page, registration, sessionId, song, status, ts, userAgent, userId

stagingsongs - num_songs, artist_id, artist_latitude, artist_longitude, artist_location, artist_name, song_id, title, duration, year

Required Steps to run the project:

1. Configuration setup  
Fill the dwh.cfg with the necessary information to start a redshift cluster

2. Run create_redshift_cluster 
Run and create the cluster

3. Run create_tables.py
Use this python file to drop and create tables

4. Run etl.py 
Run this python file to create the etl pipeline to insert data into the created tables.

5. Run test_analytics.py 
This python file to run some basic analytical queries.