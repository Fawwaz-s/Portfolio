# Portfolio
**Scenario**

Cyclistic: A bike-share program that features more than 5,800 bicycles and 600 docking stations. Cyclistic sets itself apart by also offering reclining bikes, hand tricycles, and cargo bikes, making bike-share more inclusive to people with disabilities and riders who can’t use a standard two-wheeled bike. The majority of riders opt for traditional bikes; about 8% of riders use the assistive options. Cyclistic users are more likely to ride for leisure, but about 30% use them to commute to work each day.

The director of marketing believes the company’s future success depends on maximizing the number of annual memberships. Therefore, you team want to understand how casual riders and annual members use Cyclistic bikes differently. From these insights,you will design a new marketing strategy to convert casual riders into annual members. But first, Cyclistic executives must approve your recommendations, so they must be backed up with compelling data insights and professional data visualizations.

About the company
In 2016, Cyclistic launched a successful bike-share offering. Since then, the program has grown to a fleet of 5,824 bicycles that are geotracked and locked into a network of 692 stations across Chicago. The bikes can be unlocked from one station and returned to any other station in the system anytime. Until now, Cyclistic’s marketing strategy relied on building general awareness and appealing to broad consumer segments.

One approach that helped make these things possible was the flexibility of its pricing plans: single-ride passes, full-day passes,and annual memberships. Customers who purchase single-ride or full-day passes are referred to as casual riders. Customers who purchase annual memberships are Cyclistic members.

Cyclistic’s finance analysts have concluded that annual members are much more profitable than casual riders. Although the pricing flexibility helps Cyclistic attract more customers, The director believes that maximizing the number of annual members will be key to future growth. Rather than creating a marketing campaign that targets all-new customers, The Director believes there is a very good chance to convert casual riders into members. She notes that casual riders are already aware of the Cyclistic program and have chosen Cyclistic for their mobility needs.

The Director has set a clear goal: Design marketing strategies aimed at converting casual riders into annual members. In order to do that, however, the marketing analyst team needs to better understand how annual members and casual riders differ, why casual riders would buy a membership, and how digital media could affect their marketing tactics. The Director and her team are interested in analyzing the Cyclistic historical bike trip data to identify trends. Ask Three questions will guide the future marketing program:

> How do annual members and casual riders use Cyclistic bikes differently?

> Why would casual riders buy Cyclistic annual memberships?

> How can Cyclistic use digital media to influence casual riders to become members?

You will use Cyclistic’s historical trip data to analyze and identify trends. Download the previous 12 months of Cyclistic trip data [here](https://divvy-tripdata.s3.amazonaws.com/index.html)
(Note: The datasets have a different name because Cyclistic is a fictional company. For the purposes of this case study, the datasets are appropriate and will enable you to answer the business questions. The data has been made available by Motivate International Inc. under this [license](http://https//ride.divvybikes.com/data-license-agreement) This is public data that you can use to explore how different customer types are using Cyclistic bikes. But note that data-privacy issues prohibit you from using riders’ personally identifiable information. This means that you won’t be able to connect pass purchases to credit card numbers to determine if casual riders live in the Cyclistic service area or if they have purchased multiple single passes.

_**Steps**_

Download and unzip the tripdataset from 202004 to 202303, Note.the trip dataset is different from the station_trip dataset, which is from 2013-2020. The tripdataset is a total of 35 dataset, each contains a table of 13 columns and atleast 200,000 rows. Each dataset represents the total trips for each month. We need monthly total ride,total ride by subscriber, mean ride by subscriber, total ride by member, mean ride by member.

```
Clean the dataset with spreadsheet
total_monthly_ride =count()
total_no_subscriber =countif(range,"subscriber")
total_no_member =countif(range,"member")
mean_total =average(range)
mean_subscriber =averageifs(range,range,"subscriber")
mean_member =averageifs(range,range,"member")
#The mean values were converted from timestamps to int values after running query
```
As we proceeded, the datasets became too large to be processed by spreadsheet, I decided to proceed with SQL.
```
create table july_time(
times int,
statuses varchar(40)
) #to create a new table

INSERT INTO july_time(times,statuses)
select datediff(minute, "started_at","ended_at") as timer, member_casual
from July20 #this query to calculate the time duration of different kind of customers. 

select * from july_time

select avg (times)
from july_time
where statuses = 'member' # to get the average time for member

select avg (times)
from july_time
where statuses = 'casual' #Vice versa

NOTE! #For december 2020, the average resulted negative average values
DELETE FROM dec_time WHERE times=''; #to be sure there were no empty or null value

#for Feb2021, the avg causal ride value doesn't correspond with rest of the data.
#to get a quick overview of this data, it shows many rides had large values.
select times from feb_time
where statuses = 'casual'

select time from feb_time
where statuses = 'casual' and times >300 #rides greater than 5 hours.
->this returned 120 distinct values, the same was done for values >17 hours = 81
```
This contains information on the trip tables.

Metadata for Trips Table: Variables: trip_id: ID attached to each trip taken,starttime: day and time trip started, in CST, stoptime: day and time trip ended, in CST, bikeid: ID attached to each bike, tripduration: time of trip in seconds, from_station_name: name of station where trip originated,to_station_name: name of station where trip terminated, from_station_id: ID of station where trip originated, to_station_id: ID of station where trip terminated, usertype: "Customer" is a rider who purchased a 24-Hour Pass; "Subscriber" is a rider who purchased an Annual Membership,gender: gender of rider,birthyear: birth year of rider

Notes:

Gender and birthday are only available for Subscribers
The calculated variables will be: year,total ride, trip duration(this will be converted to minutes from seconds),Customer count, Subscriber count, Male count, Female count. Note. birth year data will be collated differently

```
install.packages("tidyverse")
install.packages("dyplr")
library(tidyverse)
library(dyplr)

custom <- filter( trip13,usertype == "Customer")#to filter just customer variable
sub <- filter( trip13,usertype == "Subscriber")#to filter just subscriber variable

custom%>%
  mutate(duration=tripduration/60)->costo 
sub%>%
  mutate(duration=tripduration/60)->subs
trip13%>%
  mutate(duration=usertype/60)->snap
 #to convert durations from seconds to minutes

mean(subs$duration)
mean(costo$duration)
mean(snap$duration)
 #to get the average values

nrow(subs) 
nrow(costo)
nrow(trip13)
#to get the number of rows
```
```
#a table in the dataset had values in a way that was complicated to compute with R to correct the errors via spreadsheet will be complicated too due to the size of the dataset #I choose to go with SQL instead.

select count(column1) as total_count, avg(column5) as averages from trips
#to get the overall count and average

select count(column10) from trips where column10 ='Customer'
select count(column10) from trips where column10 ='Subscriber' 
#to get count for each client type

select column5 from trips where column10 ='Subscriber'
select column5 from trips where column10 ='Customer' 
#to outline the variables for each client type

create table scriber( column10 int ) 
create table tomer( column10 int )
#to create a table for each outlined variable

insert into scriber(column10) select column5 from trips where column10 ='Subscriber'
insert into tomer(column10) select column5 from trips where column10 ='Customer' 
#To populate new table with values

select avg(column10) from tomer
select avg(column10) from scriber
#to get the average of the variables
```
The ride data has been cleaned and aggregated, they are ready to be analysed.
>Note!, due to the file size limit on github, the meta-data for this dataset can be found [here](https://divvy-tripdata.s3.amazonaws.com/index.html)

The visualizations for this portofolio can be found [here](https://public.tableau.com/app/profile/fawaz3095/viz/BikeDashboard_16835509317600/Dashboard1)
and [here](https://public.tableau.com/app/profile/fawaz3095/viz/Bike_2Dash/Dashboard1)

**Accessment**
To answer the business questions asked:
> How do annual members and casual riders use Cyclistic bikes differently? 
From the accessment and visualisation, we can see that in the last 10 years, casual or customers spend at least 2X longer time on rides than subscribing members who on average spend about 11 to 20 minutes on rides.

> Why would casual riders buy Cyclistic annual memberships?
Given that casual riders spend significantly more time on rides compared to members, it may be prudent to consider doing promotion directed at casual users especially during the summer months, the data shows there is a consistent surge over the last 10 years that more people take casual rides compared to the other months. 


> How can Cyclistic use digital media to influence casual riders to become members?
To influence casual rider to sign up for the annual member instead of the single ride or full-day pass, a program designed to give casual riders discounts on the annual membership after they have passed a particular ride duration on a given ride. for example if a particular rider has made several rides for more than 30 minutes in the summer months, they can be eligible to earn points that can lead to discount on the annual membership subscription. This kind of program can now be advertised via different marketing and media platfroms.
