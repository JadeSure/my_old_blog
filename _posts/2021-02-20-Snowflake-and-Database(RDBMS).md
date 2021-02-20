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
Open `~/bash_profile` add command: `alias snowsql=/Applications/SnowSQL.app/Contents/MacOS/snowsql`  
`alias snowsql=/Applications/SnowSQL.app/Contents/MacOS/snowsql`
[check official document](https://docs.snowflake.com/en/user-guide/snowsql-install-config.html#installing-snowsql-on-macos-using-homebrew-cask)




