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

```Clean the dataset with spreadsheet
total_monthly_ride =count()
total_no_subscriber =countif(range,"subscriber")
total_no_member =countif(range,"member")
mean_total =average(range)
mean_subscriber =averageifs(range,range,"subscriber")
mean_member =averageifs(range,range,"member")
##The mean values were converted from timestamps to int values after running query ```
