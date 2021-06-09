# Data Modeling w/ Postgres
Udacity Data Engineering Nanodegree - Project 1

## "Sparkify" Analytics Database

### Project Description
A fact-and-dimensions database in PostgreSQL to model song play events by fictitious users with song and artist information incorporated as well.

### Objective
The fictitious company 'Sparkify' has a streaming music application. They've been collecting logs on song plays and user activity. Their analytics team requested a way to run SQL queries against the data.

### Outcome
An ETL pipeline has been constructed for processing song data and log files in order to create a fact and dimensions database for analytical querying. 

- The `songs` and `artists` tables are created by processing a subset of JSON data from http://millionsongdataset.com/
- The log files are in JSON format, they are processed to create the following:
    - table of `users`
    - table of timestamps (`time`) for expanding time attributes of the timestamps
    - the central fact table `songplays`

### Database Design

The `songplays` table is the central fact table, which records the song play events and allows for easy access to the time a song was played, the details of the song and song's artist, as well as the details of the user that played the song.

The fields in the `songplays` table are as follows:
```
start_time, user_id, level, song_id, artist_id, session_id, location, user_agent
```
The logical relationships of the `songplays` table are as follows:
- `user_id` = `users.user_id`
- `song_id` = `songs.song_id`
- `artist_id` = `artists.artist_id`
- `start_time` = `time.start_time`

Note: foreign keys are not physically enforced due to the data subset missing song and artist information.

The dimension tables are as follows and contain the following information (table name: available attributes):
- `users`: `user_id, first_name, last_name, gender, level`
- `songs`: `song_id, title, artist_id, year, duration`
- `artists`: `artist_id, name, location, latitude, longitude`
- `time`: `start_time, hour, day, week, month, year, weekday`


### Repository Files
- `create_tables.py`: script to delete and re-create tables
- `etl.py`: script to process log files
- `data/`: directory that holds song data and log files
- `sql_queries.py`: script that holds all sql queries needed
- `*.ipynb`: notebooks used to prompt and test the creation of .py scripts


### Pipeline Instructions
You can reset the database using `create_tables.py`

```bash
python create_tables.py
```

You can process the subset of logs provided in the `data/` directory by running `etl.py`

```bash
python etl.py
```

