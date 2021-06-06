# Data Modeling w/ Postgres
Udacity Data Engineering Nanodegree - Project 1

## "Sparkify" Analytics Database

### Objective
The fictitious company 'Sparkify' has a streaming music application. They've been collecting logs on song plays and user activity. Their analytics team requested a way to run SQL queries against the data.

### Outcome
An ETL pipeline has been constructed for processing song data and log files in order to create a fact table for analytical querying. The log files are in JSON format, and the processed records are stored in a Postgres database.

### Pipeline Instructions
You can reset the database using `create_tables.py`

```bash
python create_tables.py
```

You can process the subset of logs provided in the `data/` directory by running `etl.py`

```bash
python etl.py
```

### Design

The `songplays` table is the central fact table, which contains references to the following dimension tables (table name: available attributes):
- `users`: `user_id, first_name, last_name, gender, level`
- `songs`: `song_id, title, artist_id, year, duration`
- `artists`: `artist_id, name, location, latitude, longitude`
- `time`: `start_time, hour, day, week, month, year, weekday`

The fields in the songplays table are as follows:
```
start_time, user_id, level, song_id, artist_id, session_id, location, user_agent
```

The songplays table shows the song play events and allows for easy access to the time a song was played, the details of the song and song's artist, as well as the details of the user that played the song.