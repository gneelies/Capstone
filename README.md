# Capstone
Google Data Analytics Capstone

The [Google Data Analytics Professional Certificate](https://www.coursera.org/professional-certificates/google-data-analytics?utm_source=google&utm_medium=institutions&utm_campaign=gwgsite-gDigital-emprohpp-certs-launch) is an online program aimed at equipping individuals with the necessary skills to excel as data analysts. Created by Google, this program imparts essential abilities and tools crucial for a successful data analysis career, such as data cleaning, problem-solving, and data visualization.

*Benefits of the Program:*

- Developed by Google's industry experts, ensuring top-notch quality.
- Flexibility to learn at one's own pace through online courses.
- Gain practical, hands-on experience with real-world projects relevant to the industry.
- Connect with a global community of fellow learners.
- Acquire job-ready skills upon completion of the program.

The program is broken up into 8 different courses: 

**1. Foundations: Data, Data, Everywhere**

**2. Ask Questions to Make Data-Drive Decisions**

**3. Prepare Data for Exploration**

**4. Process Data from Dirty to Clean**

**5. Analyze Data to Answer Questions**

**6. Share Data Through the Art of Visualization**

**7. Data Analysis with R Programming**

**8. Google Data Analytics Capstone: Complete a Case Study**



# Google Data Analytics Professional Capstone
### Case Study 1: How Does A Bike-Share Navigate Speedy Success?


## 1. Introduction

In this case study I demonstrate the skills and insights I learned in the Google Data Analytics Professional Certificate Course.  I will use these skills to complete the tasks of a data analyst working for the fictitious bike-share company Cyclistic.  Following the data analysis process of Ask, Prepare, Process, Analyze, Share, and Act, I will complete the business task presented to me and help the company make data-driven decisions.

## 2. Scenario

The Cyclistic Director of Marketing, Lily Moreno, believes the company's future success depends on maximizing the number of annual memberships. Therefore, my team wants to understand how casual riders and annual members use Cyclistic bikes differently. From these insights, my team will design a new marketing strategy to convert casual riders into annual members. But first, Cyclistic executives must apporove our recommendations, so they must be backed up with compelling data insights and professional data visualizations.

***About The Company***:

In 2016, Cyclistic launched a successful bike-share offering. Since then, the program has grown to a fleet of 5,824 bicycles that are geotracked and locked into a network of 692 stations across Chicago. The bikes can be unlocked from one station and returned to any other station in the system anytime.

Cyclistic's appeal is that they offer flexibility in their pricing plans with single-ride passes, full-day passes, and annual memberships. Customers who purchase single-ride or full-day passes are referred to as casual riders. Customers who purchase annual memberships are Cyclistic members.

Cyclistic’s finance analysts have concluded that annual members are much more profitable than casual riders. Moreno believes there is a very good chance to convert casual riders into members.

Moreno has set a clear goal: Design marketing strategies aimed at converting casual riders into annual members. In order to do that, however, Moreno and her team are interested in analyzing the Cyclistic historical bike trip data to identify trends.

## 3. Data Analysis Process

In this case study, the six steps of the data analysis process will be used in order to solve this problem. Those 6 steps include:
1. Ask
2. Prepare
3. Process
4. Analyze
5. Share
6. Act

### Step 1: Ask
**Key Task**: Create marketing tactics aimed at converting casual riders into Cyclistic members.

So here are the analysis questions that will help in the analysis:

1. How do annual members and casual riders use Cyclistic bikes differently?
2. What are the causes that drive casual riders to buy Cyclistic annual memberships?
3. How can Cyclistic use digital media as a tool to convert casual riders to members?

For this case, Lily Moreno who is the director of marketing has assigned me as a junior data analyst to the first question: *How do annual members and casual riders use Cyclistic bikes differently?*
Guiding Question: "How do annual members and casual riders use Cyclistic bikes differently?"

Business Task: To find trends tha show how annual and casual riders use Cyclistic differently.  Use these trends to give recommendations for the marketing team to run casual riders into members.
Shareholders: Marketing team and Executive team.

### Step 2: Prepare

This step will address the data source that will be used for the analysis and the organization of the data structure.

**Data Source**:  Cyclistic’s historical trip data from Jan 2022 to Dec 2022 which is a public dataset published by Motivate International Inc. will be used to analyze and identify trends. [Click Here](https://divvy-tripdata.s3.amazonaws.com/index.html) for the dataset.

**Data Information**: In the data source, there are 12 files in total following the naming convention of *"YYYYMM-divvy-tripdata"*. Each file contains data for a specific month, including other details such as ride ID, bike type, start time, end time, start station, end station, start location, end location, and member status. The corresponding column names are:
- ride_id
- rideable_type
- started_at
- ended_at
- start_station_name
- start_station_id
- end_station_name
- end_station_id
- start_lat
- start_lng
- end_lat
- end_lng
- member_casual


**Data Location**: Data is stored in .csv files
Data is stored on secure hard drive with password protected status.

### Step 3: Process

**Tool**: Excell Power querey Google BigQuery is used to combine the total 12 files into one dataset.

#### Data Combination

Tables representing 12 CSV files have been uploaded to the 2021_tripdata dataset. To help with data combination, the following SQL query is implemented in order to combine all 12 files into a single dataset. A new table named ***"all_tripdata"*** has been generated using the following code.:

```
CREATE TABLE IF NOT EXISTS `2021_tripdata.all_tripdata` AS 
(
  SELECT * FROM '202211_tripdata`
  UNION ALL
  SELECT * FROM `202102_tripdata`
  UNION ALL
  SELECT * FROM `202103_tripdata`
  UNION ALL
  SELECT * FROM `202104_tripdata`
  UNION ALL
  SELECT * FROM `202105_tripdata`
  UNION ALL
  SELECT * FROM `202106_tripdata`
  UNION ALL
  SELECT * FROM `202107_tripdata`
  UNION ALL
  SELECT * FROM `202108_tripdata`
  UNION ALL
  SELECT * FROM `202109_tripdata`
  UNION ALL
  SELECT * FROM `202110_tripdata`
  UNION ALL
  SELECT * FROM `202111_tripdata`
  UNION ALL
  SELECT * FROM `202112_tripdata`
);
```

Then, to check the total row numbers, we perform this SQL query. The new dataset ***"all_tripdata"*** holds a total of 5,667,717 data rows encompassing the entire year:

```
SELECT COUNT(*) AS total_records
FROM `2021_tripdata.all_tripdata`;
```
We perform the following code to show the first 10 rows of the dataset in order to understand the dataset better

```
SELECT * `FROM 2021_tripdata.all_tripdata` LIMIT 10;
```
#### Data Exploration

In order to do data exploration, the first thing to do is to check the data type to observe the inconsistencies. After checking, we have seen that the entire dataset has the ride_id as the primary key:

```
SELECT column_name, data_type
FROM `2021_tripdata`.INFORMATION_SCHEMA.COLUMNS
WHERE table_name = 'all_tripdata';

```
To help ensure data cleanness, we have to check if the dataset has any null values in any column. However, it appears that there are no ***null*** values in the dataset:

```
SELECT COUNT(*) - COUNT(ride_id) ride_id,
 COUNT(*) - COUNT(rideable_type) rideable_type,
 COUNT(*) - COUNT(started_at) started_at,
 COUNT(*) - COUNT(ended_at) ended_at,
 COUNT(*) - COUNT(start_station_name) start_station_name,
 COUNT(*) - COUNT(start_station_id) start_station_id,
 COUNT(*) - COUNT(end_station_name) end_station_name,
 COUNT(*) - COUNT(end_station_id) end_station_id,
 COUNT(*) - COUNT(start_lat) start_lat,
 COUNT(*) - COUNT(start_lng) start_lng,
 COUNT(*) - COUNT(end_lat) end_lat,
 COUNT(*) - COUNT(end_lng) end_lng,
 COUNT(*) - COUNT(member_casual) member_casual
FROM `2021_tripdata.all_tripdata`;
```

After checking the null values, we also need to check if the dataset has any duplicate values. By performing this following code, it appears that we have no duplicate values:

```
SELECT COUNT(ride_id) - COUNT(DISTINCT ride_id) AS duplicate_rows
FROM `2022_tripdata.all_tripdata`;

```

Retrieve the records of the rideable_type column to see the different bike types: electric_bike, classical_bike, docked_bike

```
SELECT DISTINCT rideable_type, COUNT(rideable_type) AS trip_type
FROM `2022_tripdata.combined_data`
GROUP BY rideable_type;
```
Retrieve the records of the member_casual column to check the different member types: member, casual

```
SELECT DISTINCT member_casual, COUNT(*) AS count_member_type
FROM your_dataset_name.your_table_name
GROUP BY member_casual;
```
The trip starts and end times are indicated in the format YYYY-MM-DD hh:mm:ss UTC in the columns *"started_at"* and *"ended_at."* By introducing a new column called ***"ride_length"*** we can compute the total trip duration. It is necessary to exclude 5360 trips with a duration exceeding one day and 122283 trips with a duration less than a minute or end times earlier than start times.

Columns such as ***"day_of_week"*** and ***"month"*** can offer valuable insights into analyzing trips at various times throughout the year.

To enhance data integrity, 833064 rows with missing values in both "start_station_name" and "start_station_id" should be eliminated. Similarly, 892742 rows with missing values in both ***"end_station_name"*** and ***"end_station_id"*** and 5858 rows with missing values in both ***"end_lat"*** and ***"end_lng"*** should also be removed.

```
SELECT started_at, ended_at
FROM `2022_tripdata.all_tripdata`
LIMIT 20;

SELECT COUNT(*) AS longer_than_1_day
FROM `2022_tripdata.all_tripdata`
WHERE (
  EXTRACT(HOUR FROM (ended_at - started_at)) * 60 +
  EXTRACT(MINUTE FROM (ended_at - started_at)) +
  EXTRACT(SECOND FROM (ended_at - started_at)) / 60) >= 1440;   -- longer than 1 day - total rows = 5360

SELECT COUNT(*) AS less_than_a_minute
FROM `2022_tripdata.all_tripdata`
WHERE (
  EXTRACT(HOUR FROM (ended_at - started_at)) * 60 +
  EXTRACT(MINUTE FROM (ended_at - started_at)) +
  EXTRACT(SECOND FROM (ended_at - started_at)) / 60) <= 1;      -- less than 1 minute - total rows = 122283
```

In the dataset, there are 833,064 rows where both the ***"start_station_name"*** and ***"start_station_id"*** values are missing.

```
SELECT DISTINCT start_station_name
FROM `2022_tripdata.all_tripdata`
ORDER BY start_station_name;

SELECT COUNT(ride_id) AS start_station_null   
FROM `2022_tripdata.all_tripdata`
WHERE start_station_name IS NULL OR start_station_id IS NULL;

```

There are also 892,742 rows in which both the ***"end_station_name"*** and ***"end_station_id"*** values are absent.

```
SELECT DISTINCT end_station_name
FROM `2022_tripdata.all_tripdata`
ORDER BY end_station_name;

SELECT COUNT(ride_id) AS end_station_null
FROM `2022_tripdata.all_tripdata`
WHERE end_station_name IS NULL OR end_station_id IS NULL;

```
In the dataset, there are a total of 5,858 rows where both the ***"end_lat"*** and ***"end_lng"*** values are missing.
```
SELECT COUNT(ride_id) AS end_loc_null
FROM `2022_tripdata.all_tripdata`
WHERE end_lat IS NULL OR end_lng IS NULL;
```
#### Data Cleaning

In step, a new table will be created for cleaned data which is easier for analysis. Therefore, the following steps are implemented:

 - First, any rows containing missing values are removed from the dataset.
 - 3 new columns, namely ***"ride_length"*** to indicate the trip duration, ***"day_of_week"*** to specify the day of the week, and ***"month"*** to represent the month, are added.
 - Trips with durations less than a minute and longer than a day are excluded, leading to the removal of a total of 1,375,912 rows during this process.


Create a new table called ***"alldata_cleaned"*** with the following code:
```
CREATE TABLE IF NOT EXISTS `2022_tripdata.alldata_cleaned` AS (
  SELECT 
    a.ride_id, rideable_type, started_at, ended_at, 
    ride_length,
    CASE EXTRACT(DAYOFWEEK FROM started_at) 
      WHEN 1 THEN 'Sun'
      WHEN 2 THEN 'Mon'
      WHEN 3 THEN 'Tue'
      WHEN 4 THEN 'Wed'
      WHEN 5 THEN 'Thu'
      WHEN 6 THEN 'Fri'
      WHEN 7 THEN 'Sat'    
    END AS day_of_week,
    CASE EXTRACT(MONTH FROM started_at)
      WHEN 1 THEN 'Jan'
      WHEN 2 THEN 'Feb'
      WHEN 3 THEN 'Mar'
      WHEN 4 THEN 'Apr'
      WHEN 5 THEN 'May'
      WHEN 6 THEN 'Jun'
      WHEN 7 THEN 'Jul'
      WHEN 8 THEN 'Aug'
      WHEN 9 THEN 'Sep'
      WHEN 10 THEN 'Oct'
      WHEN 11 THEN 'Nov'
      WHEN 12 THEN 'Dec'
    END AS month,
    start_station_name, end_station_name, 
    start_lat, start_lng, end_lat, end_lng, member_casual
  FROM `2022_tripdata.all_tripdata` a
  JOIN (
    SELECT ride_id, (
      EXTRACT(HOUR FROM (ended_at - started_at)) * 60 +
      EXTRACT(MINUTE FROM (ended_at - started_at)) +
      EXTRACT(SECOND FROM (ended_at - started_at)) / 60) AS ride_length
    FROM `2022_tripdata.all_tripdata`
  ) b 
  ON a.ride_id = b.ride_id
  WHERE 
    start_station_name IS NOT NULL AND
    end_station_name IS NOT NULL AND
    end_lat IS NOT NULL AND
    end_lng IS NOT NULL AND
    ride_length > 1 AND ride_length < 1440
);
```

Set ***"ride_id"*** as the primary key for the new table and remove rows:

```
ALTER TABLE `2022_tripdata.alldata_cleaned`
ADD PRIMARY KEY(ride_id) NOT ENFORCED;

SELECT COUNT(ride_id) AS no_of_rows
FROM `2022_tripdata.alldata_cleaned`;
```
### Step 4 & 5: Analyze and Share

#### Data Analysis & Visualization

The data has been meticulously stored and prepared for thorough analysis. Relevant information was extracted from multiple tables and then effectively visualized using **Tableau**. The primary objective of this analysis is *to understand the distinct usage patterns of Cyclistic bikes between annual members and casual riders.*

To initiate this comparison, we carefully examine and compare the specific types of bikes that each group, comprising annual members and casual riders, frequently utilizes.

![TotalBikeType](Data%20Visualization/Total%20Bike%20Types.png)

The composition of Cyclistic users can be divided into two major categories: members, accounting for approximately 59.7% of the total, and casual riders, comprising the remaining 40.3%. The percentage distribution for each bike type reveals that the classic bike is the most popular among both member and casual rider groups, with the electric bike ranking second in popularity. Interestingly, docked bikes are predominantly used by casual riders and represent the least utilized bike type within the Cyclistic service.

Moving on, we delve into the analysis of trip distributions based on different time parameters. Specifically, we explore the number of trips distributed across months, days of the week, and hours of the day.

![TotalTrip](Data%20Visualization/Total%20Trips.png)

In terms of monthly trips, both casual riders and members exhibit similar patterns, with a higher number of trips occurring during the spring and summer months, and a decline during the winter season. Interestingly, the gap between casual riders and members is narrowest in the month of July during the summer.

When comparing trips based on the days of the week, it is evident that casual riders tend to take more journeys over the weekends, while members show a decline in trip frequency during the weekends compared to the rest of the weekdays.

Analyzing trips based on the hours of the day reveals distinct patterns for members and casual riders. Members display two peak periods for trips, occurring in the early morning from around 6 am to 8 am, and in the evening from around 4 pm to 8 pm. In contrast, the number of trips for casual riders steadily increases throughout the day, peaking in the evening and then gradually decreasing.

From these observations, we can infer that members may predominantly use bikes for commuting to and from work on weekdays, while casual riders utilize bikes more frequently throughout the day, particularly on weekends for leisure purposes. Both groups exhibit higher activity levels during the summer and spring months.

To understand the differences in behavior between casual and member riders, the ride duration of trips is compared in the subsequent analysis.

![RideDurationAvg](Data%20Visualization/Ride%20Duration.png)

It is important to note that casual riders tend to have longer cycling trips compared to members on average. The average journey length for members remains consistent throughout the year, week, and day. However, there are notable variations in the ride durations of casual riders. Specifically, during the spring and summer seasons, on weekends, and between 10 am and 2 pm during the day, they cover greater distances. Conversely, they have shorter trips between five and eight in the morning.

Based on these findings, it can be inferred that casual riders travel longer distances, approximately twice as much as members, but less frequently. Their longer journeys are often observed on weekends and during the day outside of typical commuting hours, particularly in the spring and summer months, suggesting that they might be cycling for recreational purposes.

To gain further insights into the differences between casual and member riders, an analysis of the starting and ending stations' locations can be conducted. By filtering and examining stations with the most trips, additional conclusions can be drawn.

![TotalTripatStartLocation](Data%20Visualization/Total%20Trips%20at%20Start%20Location.png)

Casual riders often initiate their trips from stations located near museums, parks, beaches, harbors, and aquariums, whereas members tend to start their journeys from stations in proximity to universities, residential areas, restaurants, hospitals, grocery stores, theaters, schools, banks, factories, train stations, parks, and plazas.

![TotalTripatEndLocation](Data%20Visualization/Trips%20at%20Ending%20Station.png)

A comparable pattern is evident in the ending station locations. Casual riders tend to conclude their journeys near parks, museums, and other recreational sites, while members end their trips in proximity to universities, residential, and commercial areas. This observation further supports the notion that casual riders utilize bikes primarily for leisure activities, whereas members heavily rely on them for their daily commutes.

***Here are the summary:***

*Casual Rider*

Casual riders exhibit a preference for using bikes throughout the day, with increased usage over the weekends, especially during the summer and spring seasons, for leisure activities. They tend to travel approximately twice the distance of members but take fewer trips overall.

Furthermore, casual riders commonly commence and conclude their journeys near various recreational sites, including parks, museums, coastal areas, and other leisure destinations.

*Member Rider*

Member riders prefer using bikes primarily for commuting purposes during weekdays, particularly in the summer and spring seasons, with higher usage during typical commute hours (8 am and 5 pm). They take more frequent but shorter rides compared to casual riders, with trip durations approximately half as long.

Moreover, member riders tend to start and end their bike journeys near locations such as universities, residential areas, and commercial districts, indicating their reliance on bikes for daily commuting needs.

### Step 6: Act

Following the analysis of disparities between casual and member riders, there is an opportunity to devise marketing strategies to encourage casual riders to convert into members. The following recommendations are suggested:

1. Targeted marketing campaigns could be launched during the spring and summer seasons at tourist and recreational hotspots popular among casual riders.
2. Considering that casual riders are more active on weekends and during the summer and spring, offering seasonal or weekend-only memberships might be an effective approach.
3. Since casual riders tend to have longer bike rides than members, providing discounts for extended ride durations could serve as an incentive for casual riders and possibly encourage members to also ride for longer periods.

