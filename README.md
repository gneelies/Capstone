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
Lily Moreno: Director of Marketing. Moreno is responsible for the development of campaigns and initiatives to promote the bike-share program. These may include email, social media, and other channels.

Cyclistic marketing analytics team: A team of data analysts who are responsible for collecting, analyzing, and reporting data that helps guide Cyclistic marketing strategy.

Cyclistic executive team: The notoriously detail-oriented executive team will decide whether to approve the recommended marketing program.

Stakeholder Perspective:  Rather than creating a marketing campaign that targets all-new customers, Moreno believes there is a very good chance to convert casual riders into members. She notes that casual riders are already aware of the Cyclistic program and have chosen Cyclistic for their mobility needs.



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

The first step in the prepare process was to download all of the data needed for analysis. We will be using the Cyclistic trip data for 2021 which needs to be download in 12 separate .csv files for each month of the year and stored in a dedicated folder. The data has been made available by Motivate International Inc. under license.

Data Organization:  

File naming convention: cyclistic_tripdata_YYYMM.csv

Content: Each file contains 13 fields which contain data such as ride id, rideable type, dates, geographic data etc. Data records varied.

Data security and limitations:

Data-privacy issues prohibit you from using riders’ personally identifiable information. This means that we won’t be able to connect pass purchases to credit card numbers to determine if casual riders live in the Cyclistic service area or if they have purchased multiple single passes.

Data Issues:

Data is too big to fit an Excell spreadsheet (~1,600,000 rows per sheat)
Column names are inconsistent
Data have inconsistent labels.  Some sheets use “Customer” and “Subscriber” while others use “Member” and “Casual”.
There are gaps in data – bike rides with no station starting name, or with no trip duration.


### Step 3: Process

**Tool**: Excell Power query is used to combine the total 12 files into one dataset.

Excel

To begin the data cleaning process, I opened each .csv file in excel and did the following:

Checked for and removed any duplicates.
Used the trim() function to remove unneeded spaces.
Created a new column labeled start_time to see when riders began their rides.
Created a new column labeled ride_length by subtracting the started_at column from the ended_at column.
Changed the time format to 37:30:55 to make it more readable

Considered removing any rides under 1 minute or longer than 24 hours by sorting the speadsheet, however decided not to do this – my focus was to see when riders started using the bikes.

After uploading each of the twelve files, I combined each file into one table labeled Capstone_Analysis_Casual_Annual.  In the same query, I removed each of the rows that contained null values.

I now had a single table that had all of the clean data needed for my analysis.


### Step 4: Analyze

#### Data Analysis

To begin the analysis phase, I wanted to reemphasize the business task:  How do casual riders and members use bikes differently?

Here is the main insight I discovered from my Query:

Members used the bikes more than casual riders.
Casual riders used the bikes at about the same time members used bikes!
While casual rider’s trips lasted on average longer than, the time of use was nearly the same.

I did not analyze the data for seasons or individual months, but this would have been helpful.

I now had some very important data to create visuals and begin providing business suggestions.




### Step 5: Vizualization

For my visualization, I wanted to be very specific and narrow my suggestion to one significant point.

 ![image](https://github.com/gneelies/Capstone/assets/148823383/62a3931b-54b5-4dc3-aadb-7343c308c42d)



Here are my thoughts about the key difference found between Members and Casual Riders:

Members and casual riders tend to use bikes at the same time throughout the day.
Peak times are about the same for both kinds of riders – gradual increase through the morning, except a peak at around 8 AM and Noon, but peaks in the late afternoon.

I also ran a query to see if there is any difference through out year:

![image](https://github.com/gneelies/Capstone/assets/148823383/e7f73e3c-3a79-4509-b905-b8a0e1942722)

 


It appears that both casual riders and members utilize bikes about the same time during the year and during the day.







### Step 6: Act

Based on my analysis, I came up with the following recommendations that I believe will help the marketing team create an effective campaign to convert casual riders into members:

1. Ride More:  Offer a discount to casual riders to use bikes for travel to work or school.  Since casual riders already use bikes at about the same time during the day, an emphasis on a wider range of options would be helpful.

2. Member Reachout: Give a discount to members who enlist casual riders to become members.  Give members who already enjoy the use of bikes a chance to create new ideas for casual bike riders.

By implementing these concise strategies, the marketing campaign can effectively convert casual riders into valued members, enriching their biking experience during the summer season.


