# Cyclistic_case_study

Case study https://www.coursera.org/learn/google-data-analytics-capstone

Dataset https://divvy-tripdata.s3.amazonaws.com/index.html

# Introduction

A programme for sharing bicycles that has 600 docking stations and more than 5,800 bikes. In order to make bike sharing more accessible to individuals with disabilities and others who are unable to operate a traditional two-wheeled bike, Cyclistic distinguishes itself by additionally providing cargo bikes, hand tricycles, and reclining bikes. Just 8% of riders choose the assistance choices; most riders choose regular bikes. While pleasure riding is the primary purpose for cyclists, around 30% of them use their bikes for daily commuting to work.

The financial researchers at Cyclistic have determined that annual members generate significantly higher profits than casual riders. While Cyclistic's flexible pricing helps the company draw in more clients, my manager, Moreno, the head of marketing, thinks that the secret to future success will be to maximise the number of annual members. Instead of launching a marketing effort aimed at attracting brand-new clients, Moreno thinks there's a strong possibility of turning casual riders into members. She points out that casual riders have already chosen Cyclistic for their mobility needs and are already aware of the programme.

# Scenario

At Cyclistic, a Chicago bike-share firm, I'm going to assume that I'm a junior data analyst employed in the marketing analyst team. For the organisation to succeed in the future, increasing the number of yearly memberships is crucial, according to the head of marketing. My research team therefore aims to determine the differences in cycling bike usage between annual members and casual riders. In order to turn casual riders into yearly members, my team will create a new marketing plan based on these insights. Our suggestions must, however, be supported by strong data insights and expert data visualisations in order for Cyclistic executives to approve them first.

# Analysis Process

I will use the steps of the data analysis process—ask, prepare, process, analyse, share, and act—to provide answers to the important business issues.

# Ask
Key task: Develop marketing strategies with the goal of turning casual riders into members of Cyclistic.

The following analysis questions will aid in the analysis:
1. How do annual members and casual riders use Cyclistic bikes differently?
2. Why would casual riders buy Cyclistic annual memberships?
3. How can cyclistic use digital media to influence casual riders to become members?

I was given the task of responding to Moreno's first question: How do annual memebrs and casual riders use cyclistic bikes differently?

# Prepare

The data source that will be utilised for the data structure's organisation and analysis will be covered in this step.


Data Source: To analyse and identify patterns, Motivate International Inc.'s public dataset of historical trip data from Cyclistic between January 2022 and December 2022 will be analysed. 

Data Structure: Each of the 12 files, which use the naming pattern YYYYMM-divvy-tripdata, contains data for a single month. The corresponding column names are ride_id, rideable_type, started_at, ended_at, start_station_name, start_station_id, end_station_name, end_station_id, start_lat, start_lng, end_lat, end_lng and member_casual.

# Process

Bigquery is used to combine all 12 files into a single dataset and clean it. 

# Data Combination 

In order to facilitate the combining of data, the 12 files are combined into a single dataset using the SQL query below. The code below was used to create a new table called "trips_2022_combined".

<img width="782" alt="image" src="https://github.com/AAGH98/Cyclistic_case_study/assets/141926743/aad813d8-237d-438f-a64f-8c416cd138f7">



The total number of rows are checked in the new table "trips_2022_combined" by using the query below.

<img width="506" alt="image" src="https://github.com/AAGH98/Cyclistic_case_study/assets/141926743/532e7a72-fcf6-45c1-b43b-6dc7fa522611">




# Data Exploration 

Prior to cleaning the data, the data is explored to find any inconsistencies. 

1. The table below shows all column names and their data types. ride_id is the primary key.
   
<img width="239" alt="image" src="https://github.com/AAGH98/Cyclistic_case_study/assets/141926743/52effd1a-a2a5-410b-905d-022532d9a7fc">



2. During the cleaning process, the data is checked for any null values using the query below

   <img width="531" alt="image" src="https://github.com/AAGH98/Cyclistic_case_study/assets/141926743/855e90ec-6577-435c-bb8b-0f24cc653b4b">

   

