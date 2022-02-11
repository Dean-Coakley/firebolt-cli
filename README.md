# Firebolt-CLI
Firebolt cli is a tool for connecting to firebolt, managing firebolt resources, and executing queries from the command line.

## Quickstart

### Prerequisites
`python>=3.6` and `pip` should be installed beforehand. For this go to [Python official page](https://www.python.org/downloads/). 

Also, you will need a firebolt account with information about username, password, database, and engine. For more information go to [Firebolt](https://firebolt.io).

### Installation
Once you have all prerequisites in place, you can install the firebolt cli via pip:
```
$ pip install firebolt-cli
```

To verify the installation run:
```
$ firebolt --version

firebolt, version 0.0.1
```

### Running
The next step is to configure the firebolt cli:
```
$ firebolt configure

Username [None]: your_username
Password [None]: ********
Account name [None]: your_firebolt_account_name
Database name [None]: your_database
Engine name or url [None]: your_engine_name_or_url
Created new config file
```

To run your first query, the engine has to be running. Check the status of the engine by executing the following command:
```
$ firebolt engine status --name your_engine_name

Engine your_engine_name current status is: ENGINE_STATUS_SUMMARY_STOPPED
```

If the engine is stopped, you have to start the engine by executing the following command:
```
$ firebolt engine start --name your_engine_name

Engine your_engine_name is successfully started
```

Now you are ready to run your first query, this could be done by opening the interactive query 
```
$ firebolt query

Connection succeded
firebolt> SELECT * FROM your_table LIMIT 5;
+--------------+-------------+-------------+--------------+
|   l_orderkey |   l_partkey |   l_suppkey | l_shipdate   |
+==============+=============+=============+==============+
|      5300614 |       66754 |        4273 | 1993-02-06   |
+--------------+-------------+-------------+--------------+
|      5300614 |      131772 |        6799 | 1993-02-21   |
+--------------+-------------+-------------+--------------+
|      5300615 |      106001 |        8512 | 1997-12-10   |
+--------------+-------------+-------------+--------------+
|      5300615 |      157833 |        7834 | 1997-12-01   |
+--------------+-------------+-------------+--------------+
|      5300640 |       36106 |        8610 | 1994-09-10   |
+--------------+-------------+-------------+--------------+
firebolt>
```


## Usage

With firebolt cli you can manage the databases and engines, as well as run SQL quires.
```
$ firebolt --help

Usage: firebolt [OPTIONS] COMMAND [ARGS]...

  Firebolt command line utility.

Options:
  -V, --version  Show the version and exit.
  --help         Show this message and exit.

Commands:
  configure  Store firebolt configuration parameters in config file
  database   Manage the databases
  engine     Manage the engines
  query      Execute sql queries
```
For more information about a specific command use flag `--help`, e.g. `firebolt database create --help`.

### Configure 
There are three ways to configure firebolt cli:
1. Run `firebolt configure` and setting all parameters from STDIN.

Or you can set particular parameters by running configure with additional command-line arguments:
```
firebolt configure --username your_user_name --password-file /path/to/pswd
```

2. Pass additional command-line arguments to each command.

```
firebolt query --username your_user_name --password-file /path/to/pswd
```

3. Use environment variable
```
$ export FIREBOLT_USERNAME=your_username
$ export FIREBOLT_ACCOUNT_NAME=your_account_name
$ export FIREBOLT_API_ENDPOINT=api_endpoint
$ export FIREBOLT_ENGINE_NAME_URL=your_engine_name_or_url
$ firebolt query
```
Note, that it is not possible to set the password via the environment variables directly.

### Interactive SQL
To enter interactive SQL, firebolt CLI has to be configured using one of three methods from [configuration section](#configure).
Then simply run 
```
$ firebolt query

firebolt> .help
.exit     Exit firebolt-cli
.help     Show this help message
.quit     Exit firebolt-cli
.tables   Show tables in current database
firebolt>
```

Interactive SQL mode also supports multiline commands and multiple statements;  
```
firebolt> SELECT * FROM your_table
     ...> ORDER BY l_shipdate
     ...> LIMIT 2;
+--------------+-------------+-------------+--------------+
|   l_orderkey |   l_partkey |   l_suppkey | l_shipdate   |
+==============+=============+=============+==============+
|      1552449 |      159307 |        1823 | 1992-01-02   |
+--------------+-------------+-------------+--------------+
|      5431079 |       78869 |        6391 | 1992-01-02   |
+--------------+-------------+-------------+--------------+
firebolt>
firebolt> SELECT * FROM your_table1 LIMIT 1; SELECT * FROM your_table2 LIMIT 2;
+--------------+-------------+-------------+--------------+
|   l_orderkey |   l_partkey |   l_suppkey | l_shipdate   |
+==============+=============+=============+==============+
|      5300614 |       66754 |        4273 | 1993-02-06   |
+--------------+-------------+-------------+--------------+
+-------------+--------------+
|   l_suppkey | l_shipdate   |
+=============+==============+
|        8189 | 1996-03-03   |
+-------------+--------------+
|        8656 | 1996-02-27   |
+-------------+--------------+
firebolt> 
```

### Managing resources
With firebolt cli it is also possible to manage databases and engines, for the full set of available features please see `firebolt engine --help` and `firebolt database --help`.  


## Docker 
TODO: Add docker description
