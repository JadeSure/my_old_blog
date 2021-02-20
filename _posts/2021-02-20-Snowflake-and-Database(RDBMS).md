---
layout:     post
title:      RDBMS Database with Snowflake
subtitle:   This blog includes connect snowflake by Open Command Line(CLI) in Mac, and includes some high level windows analytic function, such as dense_rank, partion by, lead, lag and so forth. 
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
5. Create Schema in the database first to recieve data from crime2.csv
```python
create or replace TABLE CRIME_LITE (
INCIDENT_NUMBER VARCHAR(15) NOT NULL,
OFFENSE_CODE VARCHAR(10) NOT NULL,
OFFENSE_CODE_GROUP VARCHAR(255) NOT NULL,
OFFENSE_DESCRIPTION VARCHAR(255),
DISTRICT VARCHAR(10),
SHOOTING VARCHAR(2),
OCCURRED_ON_DATE TIMESTAMP_NTZ(9) NOT NULL,
YEAR NUMBER(38,0) NOT NULL,
MONTH NUMBER(38,0) NOT NULL,
DAY_OF_WEEK VARCHAR(20) NOT NULL,
HOUR NUMBER(38,0) NOT NULL,
UCR_PART VARCHAR(10),
STREET VARCHAR(255)
);
```  
                                                 
6. Copy data into table
`alter warehouse &mywarehouse resume;`: if the system iterrupt, whether we need to resume the process.
```python
copy into CRIME_LITE
from @my_csv_stage/crime2.csv.gz
file_format = (format_name = CRIME_DEMO1)
on_error = 'skip_file';
```  
Then, it will show a success message with loaded process.
![picture1](/img/snowflake-file-sucess.png)


## SQL for Table vs View
Table: a table is a collection of related data held in a structured format within a database. It consists of columns, and rows.  
View: a view is a virtual table based on the result-set of an SQL statement.  
View can add one more layer for security that avoid opertation in the deep level(real database) directly.  
view can control permission.  
```python
Create view join_demo.order_validation as [select-statement]
```  
Next time, if you want to call this view: `select * from jpin_demo.order_validation`

## SQL for Index
An index is a data structure that improves the speed of data retrieval on a table at the cost of additional writes and storage to maintain it.  
It has the primary index and secondary index. By default, primary index will base on the first column --> hashcode    
eg. create index address on customer_new(Address);


## Windows Function
select [windows functino location] from ...
### RANK
DENSE_RANK: no gap in the index, same level index shows the same index value. eg. 1,2,2,2,3,4  
RANK: a gap between same level index and the next one. eg. 1,2,2,2,5,6  
ROW_NUMBER: won't consider same level index, just in order. eg. 1,2,3,4,5,6  
syntax: **DENSE_RANK/RANK/ROW_NUMBER OVER(order by order_id) AS 'dense_rank/rank/row_number'** from tabel.

### PARTITIN BY
Based one columns attributes to make a partition.  
syntax: DENSE_RANK/RANK/ROW_NUMBER **OVER(PARTITION BY COL1, order by order_id)** as partition.  

### LEAD & LAG
This function can judge the next/previous transaction for this customer (column attributes), which can be used to calculate the gap between two transactions.  
syntax:  
**LEAD(order_date, 1)** OVER (PARTITION BY First_Name, ORDER BY order_date) as next_order_date ps: 1 means the next one gap.  
**LAG(order_date, 1)** OVER (PARTITION BY First_Name, ORDER BY order_date) as prev_order_date : 1 means the previous one gap.

### Cumulative Sum & Moving Average (SQL Frame Clause)
sum value and calculate the average value.  
syntax for preceding (roll back):  
**SUM(CNT) OVER (ORDER BY ROWS_NAME ROWS BETWEEN 27 PRECEDING AND CURRENT ROW)** as CUM_CNT  (totally 28)   
**AVG(CNT) OVER (ORDER BY ROWS_NAME ROWS BETWEEN 27 PRECEDING AND CURRENT ROW)** as CUM_CNT  (totally 28)   
syntax for following (next turn):  
**SUM(CNT) OVER (ORDER BY ROWS_NAME ROWS BETWEEN CURRENT ROW AND 27 FOLLOWING)** as CUM_CNT  (totally 28)    
**AVG(CNT) OVER (ORDER BY ROWS_NAME ROWS BETWEEN CURRENT ROW AND 27 FOLLOWING)** as CUM_CNT  (totally 28)

eg. AVG(CNT) OVER (ORDER BY [ROWS_NAME] ROWS BETWEEN CURRENT 27 PRECEDING AND 27 FOLLOWING) as CUM_CNT 

Advanced syntax: SQL NTILE & Common Table Expression(CTE) Omit Now! :)

## Data Profiling?
Data retrieval, such as how many columns, empty one...

SQL fundamental exercise file(join, groupby, having...):
SQL Windows function file:



















