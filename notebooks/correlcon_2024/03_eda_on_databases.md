## aeda Usage

### 1. Clone and install the repository

Download or clone this repository and install the dependencies.

```bash
git clone https://github.com/darenasc/aeda.git
cd aeda
```

If you don't have [pipenv](https://pipenv.pypa.io/en/latest/) installed, you can install it with:

```bash
pip install pipenv
```

Then, you can install the dependencies with:

```bash
pipenv install Pipfile
```

### 2. Create a database connection file

`aeda` requires a `databases.ini` file in the `src/aeda/connection_strings/` folder to store the connections to databases. You can rename the [`databases.ini.template`](src/aeda/connection_strings/databases.ini.template) file that is included with the repo and then add your connections there. The `databases.ini` file is not syncronised with the repo.

### 3. Add database connections

The database connections have the following format. 

```ini
# databases.ini
[correlcon-aeda]
db_engine = postgres
host = 74.207.254.94
schema = public
catalog = world
user = demo
password = demo
port = 6604

[correlcon-metadata]
db_engine = postgres
host = 74.207.254.94
schema = public
catalog = metadata
user = demo
password = demo
port = 6604
metadata_database = yes
```

**`[correlcon-aeda]`** and **`[correlcon-metadata]`** are references to database connections. 

* `[correlcon-aeda]` is the database that we want to profile, and we need reading priviledges to that database. 
* `[correlcon-metadata]` is the database where we will store the metadata from `[correlcon-aeda]`. The database defined by `[correlcon-metadata]` requires writing priviledges.

The `metadata_database` parameter is optional. It is used by a `streamlit` app to show the connection and presents the `metadata_database` as a dropdown list.

The supported database engines, to fill the `db_engine` property in the `databases.ini` 
file are:

* [x] `sqlite3`
* [x] `mysql`
* [x] `postgres`
* [x] `mssqlserver`
* [x] `mariadb`
* [x] `snowflake`
* [x] `aurora`
* [x] `saphana`
* [x] `saphana_odbc`

#### 3.1. Check connections

You can check what connections are available using `list-connections` that will list the connections available. You can use the name in the `section` column to refer to that specific connection.

```bash
python aeda_.py list-connections
```

```bash
+--------------------+-----------+---------------+--------+----------+------+-------------------+
|      section       | db_engine |     host      | schema | catalog  | port | metadata_database |
+--------------------+-----------+---------------+--------+----------+------+-------------------+
| correlcon-metadata | postgres  | 74.207.254.94 | public | metadata | 6604 |        yes        |
|   correlcon-aeda   | postgres  | 74.207.254.94 | public |  world   | 6604 |                   |
+--------------------+-----------+---------------+--------+----------+------+-------------------+
```

#### 3.2 Test the connections

To test the connections to the databases you have created, you can use the 
following command:

```bash
cd src/aeda
python aeda_.py test-connection correlcon-aeda # or
python aeda_.py test-connections correlcon-aeda correlcon-metadata # list of connection names from `databases.ini` separate by spaces
```

This should print the following:

```bash
[ OK ]	postgres connection to 74.207.254.94.world.public established...
[ OK ]	postgres connection to 74.207.254.94.metadata.public established...
```

### 4. Exploring the source database

To explore a database you need to run the following command from the terminal 
in the `src/aeda` folder:

```bash
cd src/aeda
python aeda_.py explore --source correlcon-aeda --metadata correlcon-metadata
```

Where `correlcon-aeda` and `correlcon-metadata` are the names of the 
connection definitions in the `databases.ini` configuration file.

### 5. Relax and wait for the results.

The process has 6 stages and will print `Done!` when the process is finished.

The phases of the profiling are six:

1. It's going to get all the columns from the metadata.
2. It's going to compute number of columns and number of rows per table.
3. It's going to compute the number of unique values and number of `NULL` values per column.
4. It's going to compute the data value frequency per column.
5. It's going to compute the monthly frequency of the timestamp or date type columns.
6. It's going to compute statistics of the numeric type columns.

The tables are processed by number of rows, so from step 3 it's going to process the tables with less rows first.

### 6. Visualising the results

You can query the resulting database or use a minimalistic user interface 
develped with [streamlit](https://streamlit.io) from the `src/aeda/streamlit` 
folder. It will publish the report in the port `5000` of your `localhost`.

```bash
cd src/aeda/streamlit
streamlit run aeda_app.py
```