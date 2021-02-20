---
layout:     post
title:      RDBMS Database with Snowflake
subtitle:   This blog includes connect snowflake by Open Command Line(CLI) in Mac, and includes some basic SQL knowledge, such as create table(DB), left join, right join, inner join, group by, view, and index, and also some high level windows analytic function, such as dense_rank, partion by, lead, lag and so forth. 
date:       2021-02-20
author:     Shuo Wang
header-img: img/post-bg-snowflake.jpg
catalog: true
tags:
    - RDBMS DB
    - Snowflake
---


# Connect local PC into snowflake by CLI

## Installing SnowSQL on macOS Using Homebrew Cask
1. Install snowflake snowsql in the Mac  
`$ brew install --cask snowflake-snowsql`  
2. Configuring the snowsql into the terminal  
Open `~/bash_profile` add command: `alias snowsql=/Applications/SnowSQL.app/Contents/MacOS/snowsql` to set an alias to the SnowSQL executable so that you can run SnowSQL on the command line in Terminal.   
`alias snowsql=/Applications/SnowSQL.app/Contents/MacOS/snowsql`
[check official document](https://docs.snowflake.com/en/user-guide/snowsql-install-config.html#installing-snowsql-on-macos-using-homebrew-cask)

## Create Stage
1. Log on CLI in the terminal  
`snowsql -a $account_name -u &user_name -w COMPUTE_WH -d DEMO_DB -s PUBLIC`
for example, `snowsql -a ea34666.ap-southeast-2 -u tremendousure -w COMPUTE_WH -d DEMO_DB -s PUBLIC`  
(Alarm: Table name should be as same as database name, like a Capital Letter)
2. Create Stage
`CREATE STAGE "DE_DEMO"."PUBLIC"."MY_CSV_STAGE"`  
3. Create FIle Format
```python
CREATE OR Replace FILE FORMAT "DE_DEMO"."PUBLIC".CRIME_DEMO1
TYPE = 'CSV'
COMPRESSION = 'GZIP'
FIELD_DELIMITER = ','
RECORD_DELIMITER = '\n'
SKIP_HEADER = 1
FIELD_OPTIONALLY_ENCLOSED_BY = '\042'
TRIM_SPACE = TRUE
ERROR_ON_COLUMN_COUNT_MISMATCH = TRUE
ESCAPE = 'NONE'
ESCAPE_UNENCLOSED_FIELD = '\134'
DATE_FORMAT = 'AUTO'
TIMESTAMP_FORMAT = 'dd/mm/yyyy HH24:MI'
NULL_IF = ('NULL');
```
4. Put the file into stage
`put file:///Users/user/Downloads/crime2.csv @"DE_JIANGREN_DEMO"."PUBLIC"."MY_CSV_STAGE" auto_com
                                                 press=true;`
                                                 
5. Copy data into table
`alter warehouse &mywarehouse resume;`: if the system iterrupt, whether we need to resume the process.

```python
copy into CRIME_LITE
from @my_csv_stage/crime2.csv.gz
file_format = (format_name = CRIME_DEMO1)
on_error = 'skip_file';
```






