# Data Modeling with Postgres

## Introduction

The goal of this project is to build a PostgreSQL database utilizing the data on users activity and songs metadata. Building the database helps us do complex analytics regarding users activity as well as song play analysis.

## Data

The songs' metadata sourse is a subset of the [Million Song Dataset](https://labrosa.ee.columbia.edu/millionsong/). Also, the users' activities is a simulated data using [eventsim](https://github.com/Interana/eventsim). The data resides in two main directories:

- Songs metadata: collection of JSON files that describes the songs such as title, artist name, year, etc.
- Logs data: collection of JSON files where each file covers the users activities over a given day.

## Methodology

We'll build the database by optimizing the tables around efficient reads for complex queries. To do that, **Star** schema will be used utilizing dimensional modeling as follows:

- Fact table: songplays.
- Dimensions tables: songs, artist, users, time.

The three most important advantages of using Star schema are:

- Denormalized tables.
- Simplified queries.
- Fast aggregation.

## HOW TO

The source code is available in three separate **Python** scripts. Below is a brief description of the main files:

1. `sql_queries.py` has all the queries needed to both create/drop tables for the database as well as a SQL query to get song_id and artist_id from other tables since they are not provided in logs dataset.
2. `create_tables.py` creates the database, establish the connection and creates/drops all the tables required using sql_queries module.
3. `etl.py` build the pipeline that extracts the data from JSON files, does some transformation (such as adding different time attributes from timestamp) and then insert all the data into the corresponding tables.

Therefore, we first run `create_tables.py` then `etl.py` to create the database, create tables, and then insert the data using the ETL pipeline.

## Examples

```python
%load_ext sql
%sql postgresql://student:student@127.0.0.1/sparkifydb
%%sql
SELECT COUNT(*) from songplays;
```

>>> postgresql://student:***@127.0.0.1/sparkifydb

>>> 1 rows affected.

>>> Out[1]: count 6820

## License
[MIT](LICENSE)