# Cyclistic : Google Data Analytics Case Study

## Scenario:
You are a junior data analyst working in the marketing analyst team at Cyclistic, a bike-share company in Chicago. The director
of marketing believes the company’s future success depends on maximizing the number of annual memberships. Therefore,
your team wants to understand how casual riders and annual members use Cyclistic bikes differently. From these insights,
your team will design a new marketing strategy to convert casual riders into annual members. But first, Cyclistic executives
must approve your recommendations, so they must be backed up with compelling data insights and professional data
visualizations.

## About the company:
In 2016, Cyclistic launched a successful bike-share offering. Since then, the program has grown to a fleet of 5,824 bicycles that
are geotracked and locked into a network of 692 stations across Chicago. The bikes can be unlocked from one station and
returned to any other station in the system anytime.

Until now, Cyclistic’s marketing strategy relied on building general awareness and appealing to broad consumer segments.
One approach that helped make these things possible was the flexibility of its pricing plans: single-ride passes, full-day passes,
and annual memberships. Customers who purchase single-ride or full-day passes are referred to as casual riders. Customers
who purchase annual memberships are Cyclistic members.

### Note:
For learning purposes a variety of tools were used for this use case.

# Ask:
## The business task:
The business task in this case is to discover marketing strategies aimed at converting casual rides to annual riders. To achieve this, a few questions were asked:
1. How do annual members and casual riders use Cyclistic bikes differently?
2. Why would casual riders buy Cyclistic annual memberships?
3. How can Cyclistic use digital media to influence casual riders to become members?

## Stakeholders:
1. **Lily Moreno**: The director of marketing and your manager. Moreno is responsible for the development of campaigns
and initiatives to promote the bike-share program. These may include email, social media, and other channels.
2. **Cyclistic marketing analytics team:** A team of data analysts who are responsible for collecting, analyzing, and
reporting data that helps guide Cyclistic marketing strategy. You joined this team six months ago and have been busy
learning about Cyclistic’s mission and business goals — as well as how you, as a junior data analyst, can help Cyclistic
achieve them.
3. **Cyclistic executive team:** The notoriously detail-oriented executive team will decide whether to approve the
recommended marketing program.

# Prepare:
For this case study the 12 most recent months (as of Oct 2022) of Cyclistic's data was collected. The data was has been made available by Motivate International Inc and can be found [here](https://divvy-tripdata.s3.amazonaws.com/index.html), under this [license](https://ride.divvybikes.com/data-license-agreement). 

The data files have been downloaded and stored locally and on Google Drive.

All 12 spreadsheets are formatted to be CSV files (comma seperated values) and have a total of 13 identical columns. Column names are the following: ride_id, ridable_type, started_at, ended_at, start_station_name, start_station_id, end_station_name, end_station_id, start_lat, start_lng, end_lat, end_lng, member_casual.

# Process:
## Tools:
RStudios was used for the data cleaning process of this case study. This is because, R is very strong and powerful when it comes to using a large amount of data.

## Cleaning and transforming the data:
To begin, the data was imported from it's local directory. Additionally, any blank values were converted to 'N/A'.

```ruby
#importing csv files and changing all blanks to NA values
Oct_21 <- read.csv("202110-divvy-tripdata.csv", na.strings = c("", "NA"))
Nov_21 <- read.csv("202111-divvy-tripdata.csv", na.strings = c("", "NA"))
Dec_21 <- read.csv("202112-divvy-tripdata.csv", na.strings = c("", "NA"))
Jan_22 <- read.csv("202201-divvy-tripdata.csv", na.strings = c("", "NA"))
Feb_22 <- read.csv("202202-divvy-tripdata.csv", na.strings = c("", "NA"))
Mar_22 <- read.csv("202203-divvy-tripdata.csv", na.strings = c("", "NA"))
Apr_22 <- read.csv("202204-divvy-tripdata.csv", na.strings = c("", "NA"))
May_22 <- read.csv("202205-divvy-tripdata.csv", na.strings = c("", "NA"))
Jun_22 <- read.csv("202206-divvy-tripdata.csv", na.strings = c("", "NA"))
Jul_22 <- read.csv("202207-divvy-tripdata.csv", na.strings = c("", "NA"))
Aug_22 <- read.csv("202208-divvy-tripdata.csv", na.strings = c("", "NA"))
Sep_22 <- read.csv("202209-divvy-publictripdata.csv", na.strings = c("", "NA"))
```
Move forward, all sheets were combined into one.

```ruby
#combining the sheets together
Combined_trips <- bind_rows(
  Oct_21,
  Nov_21,
  Dec_21,
  Jan_22,
  Feb_22,
  Mar_22,
  Apr_22,
  May_22,
  Jun_22,
  Jul_22,
  Aug_22,
  Sep_22
)
```
In the next code chunk all uneccessary columns were dropped.

```ruby 
#removing columns that are not necessary
Combined_trips = select(-c(start_lat, start_lng, end_lat, end_lng)) 
```
Duplicates or 'N/A' values were removed.

```ruby
#removing duplicates and NA values
Combined_trips <- distinct(Combined_trips) %>%
  na.omit(Combined_trips)
```
Lastly, the file was exported (in order to use in tableau)
```ruby
write.csv(Combined_trips, "Filtered_Cyclistic_Data.csv")
```

As a result, before data cleaning there were *13 columns* and *5828235 rows*
