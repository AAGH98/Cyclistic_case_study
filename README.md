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

   
- The table below shows the number of null values in each column. 
Important observation: start_station_name and start_station_id have the same number of missing values. As well as, end_lat and end_lng. This may could be due to missing information in the same row. 

<img width="1336" alt="image" src="https://github.com/AAGH98/Cyclistic_case_study/assets/141926743/77fa4062-fbf7-44d9-84a9-f7c60cc57f5e">





3. The table is checked for any duplicates using the query below.

<img width="560" alt="image" src="https://github.com/AAGH98/Cyclistic_case_study/assets/141926743/863392ed-548f-4faa-8fca-579b644ca7a4">


- There are no duplicate rows.


4. The length of ride_id is checked to ensure no errors using the query below.

<img width="570" alt="image" src="https://github.com/AAGH98/Cyclistic_case_study/assets/141926743/cc8474cc-8d04-41cb-a739-f0c6668a836e">

- All of length 16
   

6. The rideable_type column is checked to see how many different bike types there are.

 <img width="533" alt="image" src="https://github.com/AAGH98/Cyclistic_case_study/assets/141926743/9e437b6e-14be-4d0d-ac16-895d81e6bc20">

- There are 3 different bike types.


7. The member_casual column is checked to see how many member types are available.

<img width="532" alt="image" src="https://github.com/AAGH98/Cyclistic_case_study/assets/141926743/f7407a44-84b2-44ed-a815-bdec62c69371">

- There are 2 types of riders, Casual riders and annual members


8. Started_at and ended_at columns show the start and end time of each trip. This is shown in the format YYYY-MM-DD hh:mm:ss UTC. To find the total trip duration from each trip, a new column ride_length can be created. There are 5360 trips which has duration longer than a day and 122283 trips having less than a minute duration or having end time earlier than start time so they will need to be removed. Columns 'day_of_week' and 'month' will be added as they can be helpful in analysis of trips at different times in a year.

<img width="879" alt="image" src="https://github.com/AAGH98/Cyclistic_case_study/assets/141926743/c36699b7-4913-4c18-9fe4-3044fee12e66">


9. There are 833064 rows where both start_station_name and start_station_id have missing values. They will need to be removed. 

<img width="624" alt="image" src="https://github.com/AAGH98/Cyclistic_case_study/assets/141926743/5792b826-ee6f-4f8e-9c02-8860f971feb7">


10. There are  892742 rows in where both  end_station_name and end_station_id have missing values. They will need to be removed. 

<img width="551" alt="image" src="https://github.com/AAGH98/Cyclistic_case_study/assets/141926743/a08de8d1-9806-48b3-b346-55b6efc8b42f">

11. There are 5858 rows where both end_lat and end_lng have missing values. They will need to be removed.

<img width="486" alt="image" src="https://github.com/AAGH98/Cyclistic_case_study/assets/141926743/29df5ebb-4612-467d-9b99-1123b117c671">



# Data Cleaning 

- A new table with clean data is created. This will allow the analysis process to be easier.

1. All the rows with missing values are deleted.
2. Three more columns ride_length for duration of the trip, day_of_week and month are added.
3. Trips with duration less than a minute and longer than a day are removed.

- Total 1,375,912 rows are removed in this step.


 <img width="651" alt="image" src="https://github.com/AAGH98/Cyclistic_case_study/assets/141926743/7a70642a-afe4-41dd-bb54-d69fd3015e58">
<img width="602" alt="image" src="https://github.com/AAGH98/Cyclistic_case_study/assets/141926743/d65521a7-accd-4aaa-b0a5-26c8d743d3e2">




4. The column "ride_id" is set as the primary key in the new table. And, the rows with missing values are removed.

<img width="798" alt="image" src="https://github.com/AAGH98/Cyclistic_case_study/assets/141926743/4bb70d75-c769-4d6f-bf42-300acbe8732f">


# Analyse and Share

The data has been stored efficiently and it is prepared for appropriate analysis. 
Multiple tables have been queried using SQL and they were visualised in Tableau.
The primary question is " How do annual members and casual riders use Cyclistic bikes differently 


1. Annual members and casual riders are compared by the type of bikes they are using. 


<img width="1291" alt="image" src="https://github.com/AAGH98/Cyclistic_case_study/assets/141926743/e816214e-26f5-49e9-b478-90d3cece2538">


- Annual members make up the majority of bike riders at 60%, whilst 40% are casual riders. Classic bikes are the most used which make up 39% of annual members, and 20% of casual riders. It is interesting to note that only casual riders use the docked bike, which is the least used. 


2. The total number of trips are analysed and compared by month, day of the week and hour per day.

<img width="997" alt="image" src="https://github.com/AAGH98/Cyclistic_case_study/assets/141926743/e4339870-6f4f-44e8-86ae-29b93f8b7ef4">


- Trips per month: throughout all the months of 2022, more trips occurred by annual members than casual riders. The least amount of trips were in January and February by both annual members and casual riders. Most trips occur in the summer time in July by both annual members and casual riders. Interestingly, the number of trips by casual rider decreases drastically after July. 
- Trips per day of the week: the number of trips taken by annual members starts to decrease over the weekend and the opposite occurs for casual riders. 
- Trips per hour: throughout the day, more trips are taken by annual members than casual riders. The most trips taken by annual members occur at 8am and 5PM. The number of trips taken by casual riders increases steadily from 5am to 5pm, after that trips taken by both annual members and casual riders both decrease.
- Conclusion: overall majority of the trips taken are from annual members. The most trips are taken in the summer time by annual members and casual riders. During the week, annual members may be commuting to and from work. Whilst casual riders utilise the bikes gradually through the day and particularly on the weekends for leisure purposes. 


3. The average ride length of annual members and casual riders is analysed to further investigate the difference between both these groups of riders.

<img width="996" alt="image" src="https://github.com/AAGH98/Cyclistic_case_study/assets/141926743/db222f01-0a88-4d41-8c83-ca52064cc845">

- Interestingly, casual riders have a higher duration than annual members. 
- Per month: casual riders have the highest bike durations from march to may. Annual members have a steady duration of approximately 13 minutes per ride throughout the year. 
- Per week: casual riders have the highest duration during the weekend.
- Per hour: casual riders have the longest duration between 10am to 2pm
- Conclusion:  casual riders travel longer distances than annual members but use the bikes less frequently. Casual riders make longer journeys on the weekends, in spring and summer season. Casual riders tend to use the bikes for leisure reasons.



Summary:

The key distinction between annual members and casual riders lies in their usage patterns and preferences. 

1. Casual riders : typically opt for bikes throughout the day, and their usage surges during the weekends. They display a preference for cycling during the spring and summer seasons. Also, they tend to utilise the bikes for nearly twice as long as annual members do.

2. Annual members: primarily favour the use of bikes for weekday commuting purposes. Their bike usage is concentrated during typical working hours of the day. They also particularly use the bikes during the spring and summer seasons. Also, they tend to make more frequent but shorter duration bike rides in comparison to casual riders 



# Act

After examining the differences between annual members and casual riders, it will be possible to develop marketing plans to persuade casual users to become members. Three recommendations are made:

1. In the spring and summer, targeted marketing efforts could be introduced in popular tourist and leisure destinations for casual riders.

2. Providing seasonal or weekend-only memberships could prove to be a successful strategy, given that casual riders tend to be more active on weekends and in the summer and spring.

3. Given that casual riders typically go on longer bike rides than members, offering discounts for longer ride times may incentivise casual riders and maybe motivate members to go on longer rides as well.










