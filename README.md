# OLYMPICS DATA ANALYSIS USING SQL 

## Instead of using Excel directly using the SQL Queries to retrive all the information that are related to it. 

## I have used the MySQL Workbench for this SQL Project for pulling information from the database. Initially created a table in the database and loaded the file into the database then retrived the information using the queries.
 
## Used different queries for retriving different informations from the database. I have attached the queries in the repository for the refernce you can check that for better understanding.

# 1) Creating a database
create database project;

# 2) Using the database
use project;

# 3) Checking the databases created 
show databases

# Creating a table 
CREATE TABLE `project`.`olympics` (
  `ID` VARCHAR(45) NULL,
  `Name` VARCHAR(100) NULL,
  `Sex` VARCHAR(45) NULL,
  `Age` VARCHAR(45) NULL,
  `Height` VARCHAR(45) NULL,
  `Weight` VARCHAR(45) NULL,
  `Team` VARCHAR(100) NULL,
  `NOC` VARCHAR(45) NULL,
  `Games` VARCHAR(45) NULL,
  `Year` VARCHAR(45) NULL,
  `Season` VARCHAR(45) NULL,
  `City` VARCHAR(100) NULL,
  `Sport` VARCHAR(255) NULL,
  `Event` VARCHAR(255) NULL,
  `Medal` VARCHAR(45) NULL);

# 4) To read the file in MySQL 
Load data infile "athlete_events.csv" into table olympics fields terminated by ',' 
lines terminated by '\n\r' ignore 1 lines

# 5) Selecting all the values present in the database
select * from olympics

# 5) Medals won in the year of 2016 
Select * from olympics where (Medal="Gold" OR Medal = "silver" OR Medal = "Bronze") AND Year=2016

# 6) Only in Athletics how many of them won gold medal from which team, name, year of winning
select * from olympics where sport ="Athletics" AND Medal =("Gold") OR Medal="Silver" OR Medal ="Bronze"

# 7) Players only from the indian team 
select * from olympics where Team = "India"

# 8) Team only from China, India and United States
select * from olympics where Team in ("China", "India", "United States")

# 9) Sport held between the year 2012-2016 
select * from olympics where year between 2012 and 2016 and Medal= "Gold" and Sex ="M" order by ID

# 10) Only select the different sports
select  distinct(sport) from olympics

# 11) To find in which event india has won the highest medals?
SELECT event,COUNT(medal)
FROM olympics
WHERE team='India'
AND medal <> 'NA'
GROUP BY event
ORDER BY COUNT(medal) DESC;

# 12) Identify the event which was played most consecutively in the summer Olympics games?
SELECT event, COUNT( event)
FROM olympics
WHERE season='Summer'
GROUP BY event
ORDER BY COUNT(event) DESC;

# 13) Which country have won most medals
SELECT noc,COUNT(medal)
FROM olympics
WHERE medal<> 'NA'
GROUP BY noc
ORDER BY COUNT(medal) desc;

# 14) Which countries won maximum medal in one year and in which year
SELECT noc, year, COUNT(medal) AS total_medals
FROM olympics
WHERE medal <> 'NA'
GROUP BY noc, year
ORDER BY total_medals DESC
LIMIT 1;


# 15) For deleting the table olympics
drop table olympics

# 16) For deleting the database
drop database project
