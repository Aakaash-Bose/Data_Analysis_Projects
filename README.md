### Cyclistic-Bikeshare_Google_Data_Analytics-Capstone
_This document is created as part of the capstone project of the Google Data Analytics Professional Certificate._
________________________________________________________________________________________________________________

**INTRODUCTION/SCENARIO**

You are a junior data analyst working in the marketing analyst team at Cyclistic, a bike-share company in Chicago. The director of marketing believes the company’s future success depends on maximizing the number of annual memberships. Therefore, your team wants to understand how casual riders and annual members use Cyclistic bikes differently. From these insights, your team will design a new marketing strategy to convert casual riders into annual members. But first, Cyclistic executives must approve your recommendations, so they must be backed up with compelling data insights and professional data visualizations.

About the organization:

Cyclistic launched a successful bike-share offering. Since then, the program has grown to a fleet of 5,824 bicycles that are geo-tracked and locked into a network of 692 stations across Chicago. The bikes can be unlocked from one station and returned to any other station in the system anytime.
The project follows the six-step data analysis process: ask, prepare, process, analyze, share, and act.
________________________________________________________________________________________________________________

1. **ASK**

A. What is the problem that requires to be solved?

Business Objective: The business objective provided by Cyclistic involves the use of creating design strategies aimed at converting casual riders into annual members.

Business Task: The business task allocated as a Junior Data Analyst is to provide insights and strategic recommendations to answer the question – ‘How do annual members and casual members use Cyclistic bikes differently?’ The new marketing strategy employed by the Marketing Analytics Team at Cyclistic is tasked with recognizing the differences in patterns based on Casual and Annual Members to understand the differences in bike usage.
Stakeholders Involved: This project consists of the following stakeholders categorized below into primary and secondary stakeholders.

Primary Stakeholder(s): 
•	Lily Moreno: Director of Marketing at Cyclistic (The Junior Data Analyst reports to this stakeholder)
•	Marketing Analyst Team at Cyclistic: This team is responsible for collecting, analyzing, and reporting the data. As a Junior Data Analyst, I am a part of this team and will work to answer the project goal.

Secondary Stakeholder(s): 
•	Executive Management Team at Cyclistic: The executive body makes the final decision on the marketing strategies provided and if these will be implemented.

B.	How will the insights drive business decisions?

The following information is required to understand what the steps are to take in the next phase of this analysis:
i)	What part of the dataset would be required for analysis?
ii)	Is the data trustworthy?
iii)	What is the best process to analyze the data?
iv)	What aspects of the historical data is required for the analysis?
v)	Why are casual riders not buying annual memberships?
vi)	How is the data being governed for privacy and safety?

Cyclistic currently has the following numbers to depict the number of bikes and docking stations accessible in the fleet:
________________________________________________________________________________________________________________

2. PREPARE

A. What are the specifics of the data provided?

i)	LOCATION OF THE DATA:

The dataset(s) provided are downloaded from https://divvy-tripdata.s3.amazonaws.com/index.html. The above link contains the data collected by Motivate Inc. responsible for collecting the user date on a monthly basis managing the City of Chicago’s bike user data. 

ii)	STRUCTURE OF THE DATA:

The data obtained is stored in .csv file format, that is updated on a monthly basis. For this project, the last twelve months of data ranging from September 2021 – August 2022 was used. Each dataset contains 13 columns containing the following information:
a.	ride_id,
b.	rideable_type,
c.	started_at,
d.	ended_at,
e.	start_station_name
f.	start_station_id,
g.	end_station_name,
h.	end_station_id,
i.	start_lat,
j.	start_lng,
k.	end_lat,
l.	end_lng,
m.	member_casual

iii) APPROACH

The ROCCC approach has been utilized to determine the credibility of the data.

Reliable – It is complete and accurate and it represents all bike rides taken in the city of Chicago for the selected duration of our analysis.

Original - The data is made available by Motivate International Inc. which operates the city of Chicago’s Divvy bicycle sharing service.

Comprehensive - the data includes all information about ride details including starting time, ending time, station name, station ID, type of membership and many more.

Current – It is up-to-date as it includes data until end of August 2022.

Cited - The data is cited and is available under Data License Agreement.

iv)	LICENSE AGREEMENT AND DATA PRIVACY

All personal information has been anonymized from the dataset(s), thereby protecting the user’s privacy. Due to the lack of user information, there is insufficient information indicating whether a casual rider uses the bikes on a repeated basis. This licence https://ride.divvybikes.com/data-license-agreement governs the distribution of this data.

v)	ERRORS IN THE DATASET

The following errors have been found in the structure of the datasets:
a.	Duplicate Records (ride_id),
b.	Missing Values (start_station, end_station, start_lat, start_lng, end_lat, end_lng)
c.	Irregularities in the following:
i.	Ride Length
ii.	Latitude and Longitude 
These can be resolved through data cleansing and the rest of the data can be filtered to support the analysis.

B.	What tool(s) are involved in this process?

Due to the large file size of the dataset(s), RStudio Desktop is being used. The dataset(s) crashed on the RStudio cloud (allowing a maximum of 3 dataset(s) out of 12 to be loaded).
RStudio acts as a one-stop shop to filter, transform, clean, and visualize data under a single platform.
________________________________________________________________________________________________________________

3. PROCESS

Load the correct and necessary libraries in RStudio:
a.	library(tidyverse)
b.	library(lubridate)
c.	library(janitor)
d.	library(dplyr)

```
>library(tidyverse)
___Attaching packages___________________tidyverse 1.3.2________
-ggplot2 3.3.6
-tibble 3.1.8
-tidyr 1.2.0
-readr 2.1.2
-purr 0.3.4
-dplyr 1.0.9
-stringr 1.4.0
-forcats 0.5.1
___Conflicts_____________________________tidyverse(conflicts)____
-dplyr:: filter()
-dplyr:: lag()
-masks stats:: filter()
-masks stats:: lag()
```
```
> library(lubridate)
> detach ("package:lubridate", unload = TRUE)
   Warning message:
                  ‘lubridate’ namespace cannot be unloaded:
                  namespace ‘lubridate’ is imported by ‘tidyverse’ so cannot be unloaded
```
```
> library(janitor)
              Attaching package: ‘janitor’
                               The following objects are masked from ‘package:stats’:
    	                       chisq.test, fisher.test
```
```
> library(dplyr)
               Attaching package: ‘dplyr’
                                The following objects are masked from ‘package:stats’:
                                 filter, lag
                                 The following objects are masked from ‘package:base’:
                                    intersect, setdiff, setequal, union
```

Upload and rename the 12 dataset(s)in RStudio:
Upload each dataset into RStudio and rename the file name as shown below:

September 2021
```
> library(readr)
> Sep21 <- read_csv("Desktop/Data_Analytics/Cyclistic/202109-divvy-tripdata/202109-divvy- tripdata.csv")
```
```
Rows: 756147 Columns: 13                                                                                                   
── Column specification ────────────────────────────────────────────────────────────────
Delimiter: ","
chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_station_...
dbl  (4): start_lat, start_lng, end_lat, end_lng
dttm (2): started_at, ended_at

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
> View(Sep21)
```

October 2021
```
> library(readr)
> Oct21 <- read_csv("Desktop/Data_Analytics/Cyclistic/202110-divvy-tripdata/202110-divvy-tripdata.csv")
```
```
Rows: 631226 Columns: 13                                                                                                   
── Column specification ────────────────────────────────────────────────────────────────
Delimiter: ","
chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_station_...
dbl  (4): start_lat, start_lng, end_lat, end_lng
dttm (2): started_at, ended_at

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
> View(Oct21)
```

November 2021
```
> library(readr)
> Nov21 <- read_csv("Desktop/Data_Analytics/Cyclistic/202111-divvy-tripdata/202111-divvy-tripdata.csv")
```
```
Rows: 359978 Columns: 13                                                                                                   
── Column specification ────────────────────────────────────────────────────────────────
Delimiter: ","
chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_station_...
dbl  (4): start_lat, start_lng, end_lat, end_lng
dttm (2): started_at, ended_at

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
> View(Nov21)
```

December 2021
```
> library(readr)
> Dec21 <- read_csv("Desktop/Data_Analytics/Cyclistic/202112-divvy-tripdata/202112-divvy-tripdata.csv")
```
```
Rows: 247540 Columns: 13                                                                                                   
── Column specification ────────────────────────────────────────────────────────────────
Delimiter: ","
chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_station_...
dbl  (4): start_lat, start_lng, end_lat, end_lng
dttm (2): started_at, ended_at

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
> View(Dec21)
```

January 2022
```
> library(readr)
> Jan22 <- read_csv("Desktop/Data_Analytics/Cyclistic/202201-divvy-tripdata/202201-divvy-tripdata.csv")
```
```
Rows: 103770 Columns: 13                                                                                                   
── Column specification ────────────────────────────────────────────────────────────────
Delimiter: ","
chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_station_...
dbl  (4): start_lat, start_lng, end_lat, end_lng
dttm (2): started_at, ended_at

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
> View(Jan22)
```

February 2022
```
> library(readr)
> Feb22 <- read_csv("Desktop/Data_Analytics/Cyclistic/202202-divvy-tripdata/202202-divvy-tripdata.csv")
```
```
Rows: 115609 Columns: 13                                                                                                   
── Column specification ────────────────────────────────────────────────────────────────
Delimiter: ","
chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_station_...
dbl  (4): start_lat, start_lng, end_lat, end_lng
dttm (2): started_at, ended_at

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
> View(Feb22)
```

March 2022
```
> library(readr)
> Mar22 <- read_csv("Desktop/Data_Analytics/Cyclistic/202203-divvy-tripdata/202203-divvy-tripdata.csv")
```
```
Rows: 284042 Columns: 13                                                                                                                                                   
── Column specification ────────────────────────────────────────────────────────────────
Delimiter: ","
chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_station_name, end_station_id, member_casual
dbl  (4): start_lat, start_lng, end_lat, end_lng
dttm (2): started_at, ended_at

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
> View(Mar22)
```

April 2022
```
> library(readr)
> Apr22 <- read_csv("Desktop/Data_Analytics/Cyclistic/202204-divvy-tripdata/202204-divvy-tripdata.csv")
```
```
Rows: 371249 Columns: 13                                                                                                   
── Column specification ────────────────────────────────────────────────────────────────
Delimiter: ","
chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_station_...
dbl  (4): start_lat, start_lng, end_lat, end_lng
dttm (2): started_at, ended_at

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
> View(Apr22)
```

May 2022
```
> library(readr)
> May22 <- read_csv("Desktop/Data_Analytics/Cyclistic/202205-divvy-tripdata/202205-divvy-tripdata.csv")
```
```
Rows: 634858 Columns: 13                                                                                                   
── Column specification ────────────────────────────────────────────────────────────────
Delimiter: ","
chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_station_...
dbl  (4): start_lat, start_lng, end_lat, end_lng
dttm (2): started_at, ended_at

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
> View(May22)
```

June 2022
```
> library(readr)
> Jun22 <- read_csv("Desktop/Data_Analytics/Cyclistic/202206-divvy-tripdata/202206-divvy-tripdata.csv")
```
```
Rows: 769204 Columns: 13                                                                                                                                                   
── Column specification ────────────────────────────────────────────────────────────────
Delimiter: ","
chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_station_name, end_station_id, member_casual
dbl  (4): start_lat, start_lng, end_lat, end_lng
dttm (2): started_at, ended_at

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
> View(Jun22)
```

July 2022
```
> library(readr)
> Jul22 <- read_csv("Desktop/Data_Analytics/Cyclistic/202207-divvy-tripdata/202207-divvy-tripdata.csv")
```
```
Rows: 823488 Columns: 13                                                                                                                                                   
── Column specification ────────────────────────────────────────────────────────────────
Delimiter: ","
chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_station_name, end_station_id, member_casual
dbl  (4): start_lat, start_lng, end_lat, end_lng
dttm (2): started_at, ended_at

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
> View(Jul22)
```

August 2022
```
> library(readr)
> Aug22 <- read_csv("Desktop/Data_Analytics/Cyclistic/202208-divvy-tripdata/202208-divvy-tripdata.csv")
```
```
Rows: 785932 Columns: 13                                                                                                                                                   
── Column specification ────────────────────────────────────────────────────────────────
Delimiter: ","
chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_station_name, end_station_id, member_casual
dbl  (4): start_lat, start_lng, end_lat, end_lng
dttm (2): started_at, ended_at

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
> View(Aug22)
```
Merge dataset(s) into one large dataset (for easier analysis)
Merged the 12 dataset(s) into one final dataset using the rbind function and named it cyc_bike as shown below:
```
cyc_bike <- rbind(Sep21, Oct21, Nov21, Dec21, Jan22, Feb22, Mar22, Apr22, May22, Jun22, Jul22, Aug22)
```

Create a backup of the final dataset
```
cyc_bikefinal <- cyc_bike
```

Addition of relevant columns.
The following columns were added to support the analysis of the final dataset.
```
cyc_bikefinal$date <- as.Date(cyc_bikefinal$started_at)  #adds a date column
cyc_bikefinal$month <- format(as.Date(bike_data$started_at), "%b_%y")  #add a month_year column (formatted as Month_XX(Year))
cyc_bikefinal$day <- format(as.Date(cyc_bikefinal$date), "%d")  #adds a day column
cyc_bikefinal$year <- format(as.Date(cyc_bikefinal$date), "%Y")  #adds a year column
cyc_bikefinal$weekday <- format(as.Date(cyc_bikefinal$date), "%A")  #adds a day of week column
cyc_bikefinal$time <- format(cyc_bikefinal$started_at, format = "%H:%M")  #adds a time started column
cyc_bikefinal$time <- as.POSIXct(cyc_bikefinal$time, format = "%H:%M")  #time format manupulation as per the user
cyc_bikefinal$ride_length <- (as.double(difftime(cyc_bikefinal$ended_at, cyc_bikefinal$started_at))) /60  #calculates the ride length in minutes
```

Look at the specifics of the dataset.

```
str(cyc_bikefinal)  #check the structure of the data

spec_tbl_df [5,883,043 × 20] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
$ ride_id           : chr [1:5883043] "9DC7B962304CBFD8" "F930E2C6872D6B32" "6EF72137900BB910" "78D1DE133B3DBF55" ...
$ rideable_type     : chr [1:5883043] "electric_bike" "electric_bike" "electric_bike" "electric_bike" ...
$ started_at        : POSIXct[1:5883043], format: "2021-09-28 16:07:10" "2021-09-28 14:24:51" "2021-09-28 00:20:16" "2021-09-28 14:51:17" ...
$ ended_at          : POSIXct[1:5883043], format: "2021-09-28 16:09:54" "2021-09-28 14:40:05" "2021-09-28 00:23:57" "2021-09-28 15:00:06" ...
$ start_station_name: chr [1:5883043] NA NA NA NA ...
$ start_station_id  : chr [1:5883043] NA NA NA NA ...
$ end_station_name  : chr [1:5883043] NA NA NA NA ...
$ end_station_id    : chr [1:5883043] NA NA NA NA ...
$ start_lat         : num [1:5883043] 41.9 41.9 41.8 41.8 41.9 ...
$ start_lng         : num [1:5883043] -87.7 -87.6 -87.7 -87.7 -87.7 ...
$ end_lat           : num [1:5883043] 41.9 42 41.8 41.8 41.9 ...
$ end_lng           : num [1:5883043] -87.7 -87.7 -87.7 -87.7 -87.7 ...
$ member_casual     : chr [1:5883043] "casual" "casual" "casual" "casual" ...
$ date              : Date[1:5883043], format: "2021-09-28" "2021-09-28" "2021-09-28" "2021-09-28" ...
$ month             : chr [1:5883043] "Sep_21" "Sep_21" "Sep_21" "Sep_21" ...
$ day               : chr [1:5883043] "28" "28" "28" "28" ...
$ year              : chr [1:5883043] "2021" "2021" "2021" "2021" ...
$ weekday           : chr [1:5883043] "Tuesday" "Tuesday" "Tuesday" "Tuesday" ...
$ time              : POSIXct[1:5883043], format: "2022-09-20 16:07:00" "2022-09-20 14:24:00" "2022-09-20 00:20:00" "2022-09-20 14:51:00" ...
$ ride_length       : num [1:5883043] 2.73 15.23 3.68 8.82 10.53 ...
- attr(*, "spec")=
  .. cols(
  ..   ride_id = col_character(),
  ..   rideable_type = col_character(),
  ..   started_at = col_datetime(format = ""),
  ..   ended_at = col_datetime(format = ""),
  ..   start_station_name = col_character(),
  ..   start_station_id = col_character(),
  ..   end_station_name = col_character(),
  ..   end_station_id = col_character(),
  ..   start_lat = col_double(),
  ..   start_lng = col_double(),
  ..   end_lat = col_double(),
  ..   end_lng = col_double(),
  ..   member_casual = col_character()
  .. )
 - attr(*, "problems")=<externalptr> 
```
```
colnames(cyc_bikefinal)  #check the column names

[1] "ride_id"            "rideable_type"      "started_at"         "ended_at"           "start_station_name" "start_station_id"  
[7] "end_station_name"   "end_station_id"     "start_lat"          "start_lng"          "end_lat"            "end_lng"           
[13] "member_casual"      "date"               "month"              "day"                "year"               "weekday"           
[19] "time" 
```
```
dim(cyc_bikefinal)  #check dimensions of the data

## [1] 5883043      20
```
```
nrow(cyc_bikefinal)  #check the number of rows

## [1] 5883043
```
```
summary(cyc_bikefinal)  #summary for the data

ride_id          rideable_type        started_at                        ended_at                      start_station_name
Length:5883043     Length:5883043     Min.   :2021-09-01 00:00:06.00   Min.   :2021-09-01 00:00:41.00   Length:5883043    
Class :character   Class :character   1st Qu.:2021-11-06 13:47:33.00   1st Qu.:2021-11-06 14:07:58.50   Class :character  
Mode  :character   Mode  :character   Median :2022-05-07 12:30:47.00   Median :2022-05-07 12:52:55.00   Mode  :character  
                                       Mean   :2022-03-22 05:41:41.57   Mean   :2022-03-22 06:01:26.78                     
                                       3rd Qu.:2022-07-06 16:00:29.50   3rd Qu.:2022-07-06 16:18:47.00                     
                                       Max.   :2022-08-31 23:59:39.00   Max.   :2022-09-06 21:49:04.00                                                                                                                                                
 start_station_id   end_station_name   end_station_id       start_lat       start_lng         end_lat         end_lng      
 Length:5883043     Length:5883043     Length:5883043     Min.   :41.64   Min.   :-87.84   Min.   :41.39   Min.   :-88.97  
 Class :character   Class :character   Class :character   1st Qu.:41.88   1st Qu.:-87.66   1st Qu.:41.88   1st Qu.:-87.66  
 Mode  :character   Mode  :character   Mode  :character   Median :41.90   Median :-87.64   Median :41.90   Median :-87.64  
                                                          Mean   :41.90   Mean   :-87.65   Mean   :41.90   Mean   :-87.65  
                                                          3rd Qu.:41.93   3rd Qu.:-87.63   3rd Qu.:41.93   3rd Qu.:-87.63  
                                                          Max.   :45.64   Max.   :-73.80   Max.   :42.37   Max.   :-87.50  
                                                                                           NA's   :5727    NA's   :5727    
 member_casual           date               month               day                year             weekday         
 Length:5883043     Min.   :2021-09-01   Length:5883043     Length:5883043     Length:5883043     Length:5883043    
 Class :character   1st Qu.:2021-11-06   Class :character   Class :character   Class :character   Class :character  
 Mode  :character   Median :2022-05-07   Mode  :character   Mode  :character   Mode  :character   Mode  :character  
                    Mean   :2022-03-21                                                                              
                    3rd Qu.:2022-07-06                                                                              
                    Max.   :2022-08-31                                                                              
 time                           ride_length      
 Min.   :2022-09-20 00:00:00.00   Min.   : -137.42  
 1st Qu.:2022-09-20 11:25:00.00   1st Qu.:    6.05  
 Median :2022-09-20 15:33:00.00   Median :   10.72  
 Mean   :2022-09-20 14:42:57.46   Mean   :   19.75  
 3rd Qu.:2022-09-20 18:21:00.00   3rd Qu.:   19.33  
 Max.   :2022-09-20 23:59:00.00   Max.   :40705.02
```

DATA CLEANING
```
cyc_bikefinal <- distinct(cyc_bikefinal)  #remove any duplicates
cyc_bikefinal <- cyc_bikefinal[! cyc_bikefinal $ride_length<1,] #get rid of negative rides
cyc_bikefinal <- cyc_bikefinal[! cyc_bikefinal $ride_length>1440,] #get rid of too long rides - rides should be limited to 1 day or 1440 minutes
```
#change a few column names for clarification
```
cyc_bikefinal <- rename(cyc_bikefinal, member_casual = customer_type) 
cyc_bikefinal <- rename(cyc_bikefinal, rideable_type = bike_type)
```
## Filter out data we will not be using and remove missing data
```
cyc_bikefinal <- cyc_bikefinal %>% select(bike_type, customer_type, started_at, date, month, day, year, weekday, time, ride_length)
drop_na(cyc_bikefinal)
```
```
A tibble: 5,767,146 × 10
   bike_type     customer_type started_at          date       month  day   year  weekday time                ride_length
   <chr>         <chr>         <dttm>              <date>     <chr>  <chr> <chr> <chr>   <dttm>                    <dbl>
 1 electric_bike casual        2021-09-28 16:07:10 2021-09-28 Sep_21 28    2021  Tuesday 2022-09-20 16:07:00        2.73
 2 electric_bike casual        2021-09-28 14:24:51 2021-09-28 Sep_21 28    2021  Tuesday 2022-09-20 14:24:00       15.2 
 3 electric_bike casual        2021-09-28 00:20:16 2021-09-28 Sep_21 28    2021  Tuesday 2022-09-20 00:20:00        3.68
 4 electric_bike casual        2021-09-28 14:51:17 2021-09-28 Sep_21 28    2021  Tuesday 2022-09-20 14:51:00        8.82
 5 electric_bike casual        2021-09-28 09:53:12 2021-09-28 Sep_21 28    2021  Tuesday 2022-09-20 09:53:00       10.5 
 6 electric_bike casual        2021-09-28 01:53:18 2021-09-28 Sep_21 28    2021  Tuesday 2022-09-20 01:53:00        6.73
 7 electric_bike casual        2021-09-28 07:15:56 2021-09-28 Sep_21 28    2021  Tuesday 2022-09-20 07:15:00       22.5 
 8 electric_bike casual        2021-09-28 11:17:00 2021-09-28 Sep_21 28    2021  Tuesday 2022-09-20 11:17:00       23.3 
 9 electric_bike casual        2021-09-27 19:57:09 2021-09-27 Sep_21 27    2021  Monday  2022-09-20 19:57:00       12.0 
10 electric_bike casual        2021-09-28 11:01:26 2021-09-28 Sep_21 28    2021  Tuesday 2022-09-20 11:01:00       21.5 
 … with 5,767,136 more rows
ℹ Use `print(n = ...)` to see more rows
```
```
remove_empty(cyc_bikefinal)
```
```
value for "which" not specified, defaulting to c("rows", "cols")
A tibble: 5,292,949 × 10
    bike_type     customer_type started_at          date       month  day   year 
    <chr>         <chr>         <dttm>              <date>     <chr>  <chr> <chr>
  1 electric_bike casual        2020-11-01 13:36:00 2020-11-01 Nov_20 01    2020 
  2 electric_bike casual        2020-11-01 10:03:26 2020-11-01 Nov_20 01    2020 
  3 electric_bike casual        2020-11-01 00:34:05 2020-11-01 Nov_20 01    2020 
  4 electric_bike casual        2020-11-01 00:45:16 2020-11-01 Nov_20 01    2020 
  5 electric_bike casual        2020-11-01 15:43:25 2020-11-01 Nov_20 01    2020 
  6 electric_bike casual        2020-11-14 15:55:17 2020-11-14 Nov_20 14    2020 
  7 electric_bike casual        2020-11-14 16:47:29 2020-11-14 Nov_20 14    2020 
  8 electric_bike casual        2020-11-14 16:04:15 2020-11-14 Nov_20 14    2020 
  9 electric_bike casual        2020-11-14 16:24:09 2020-11-14 Nov_20 14    2020 
 10 electric_bike casual        2020-11-14 01:24:22 2020-11-14 Nov_20 14    2020 
  … with 5,292,939 more rows, and 3 more variables: weekday <chr>, time <dttm>,
  ride_length <dbl>
```
```
remove_missing(cyc_bikefinal) 
```
```
A tibble: 5,767,146 × 10
   bike_type     customer_type started_at          date       month  day   year  weekday time                ride_length
   <chr>         <chr>         <dttm>              <date>     <chr>  <chr> <chr> <chr>   <dttm>                    <dbl>
 1 electric_bike casual        2021-09-28 16:07:10 2021-09-28 Sep_21 28    2021  Tuesday 2022-09-20 16:07:00        2.73
 2 electric_bike casual        2021-09-28 14:24:51 2021-09-28 Sep_21 28    2021  Tuesday 2022-09-20 14:24:00       15.2 
 3 electric_bike casual        2021-09-28 00:20:16 2021-09-28 Sep_21 28    2021  Tuesday 2022-09-20 00:20:00        3.68
 4 electric_bike casual        2021-09-28 14:51:17 2021-09-28 Sep_21 28    2021  Tuesday 2022-09-20 14:51:00        8.82
 5 electric_bike casual        2021-09-28 09:53:12 2021-09-28 Sep_21 28    2021  Tuesday 2022-09-20 09:53:00       10.5 
 6 electric_bike casual        2021-09-28 01:53:18 2021-09-28 Sep_21 28    2021  Tuesday 2022-09-20 01:53:00        6.73
 7 electric_bike casual        2021-09-28 07:15:56 2021-09-28 Sep_21 28    2021  Tuesday 2022-09-20 07:15:00       22.5 
 8 electric_bike casual        2021-09-28 11:17:00 2021-09-28 Sep_21 28    2021  Tuesday 2022-09-20 11:17:00       23.3 
 9 electric_bike casual        2021-09-27 19:57:09 2021-09-27 Sep_21 27    2021  Monday  2022-09-20 19:57:00       12.0 
10 electric_bike casual        2021-09-28 11:01:26 2021-09-28 Sep_21 28    2021  Tuesday 2022-09-20 11:01:00       21.5 
… with 5,767,136 more rows
ℹ Use `print(n = ...)` to see more rows
```
Setting the Data in order.

#this will help keep the results of the analysis in order based on the day of the week and by month to avoid confusion
```
cyc_bikefinal$weekday <- ordered(cyc_bikefinal $weekday, levels=c("Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"))
cyc_bikefinal$month <- ordered(cyc_bikefinal $month, levels=c("Sep21", "Oct21", "Nov21", "Dec21", "Jan22", "Feb22",  "Mar_22", "Apr_22","May_22", "Jun_22", "Jul_22", "Aug_22"))
```

4. **ANALYZE**
________________________________________________________________________________________________________________

shows the min, max, median, and average ride lengths
```
summary(cyc_bikefinal$ride_length)  
```
```
Min.  1st Qu.   Median     Mean   3rd Qu.    Max. 
1.000    6.283   10.933   17.323   19.550 1439.950  
```
looks at the total number of customers broken down by membership details
```
table(cyc_bikefinal$customer_type)
```
```
casual  member 
2420050 3347096
```
looks at total rides for each customer type in minutes
```
setNames(aggregate(ride_length ~ customer_type, cyc_bikefinal, sum), c("customer_type", "total_ride_length(mins)"))
```
```
customer_type total_ride_length(mins)
1        casual                56980368
2        member                42921119
```
look at ride lengths broken down by day of week and customer type
```
aggregate(cyc_bikefinal$ride_length ~ cyc_bikefinal$customer_type + cyc_bikefinal$weekday, FUN = median)   
cyc_bikefinal$customer_type cyc_bikefinal$weekday cyc_bikefinal$ride_length

1                       casual                Monday                 14.15000
2                       member                Monday                  8.78333
3                       casual               Tuesday                 12.41666
4                       member               Tuesday                  8.71666
5                       casual             Wednesday                 12.41666
6                       member             Wednesday                  8.86666
7                       casual              Thursday                 12.65000
8                       member              Thursday                  8.88333
9                       casual                Friday                 13.45000
10                      member                Friday                  9.00000
11                      casual              Saturday                 16.13333
12                      member              Saturday                 10.25000
13                      casual                Sunday                 16.50000
14                      member                Sunday                 10.06666

look at the total number of rides and averages based on the day of the week and customer type

A tibble: 14 × 4

Groups:   customer_type [2]
customer_type weekday   total_rides avg_ride
<chr>         <ord>           <int>    <dbl>
1 casual        Monday         286437     24.2
2 member        Monday         465878     12.4
3 casual        Tuesday        272459     20.8
4 member        Tuesday        526176     12.1
5 casual        Wednesday      287654     20.2
6 member        Wednesday      536405     12.2
7 casual        Thursday       305563     20.8
8 member        Thursday       515451     12.3
9 casual        Friday         339277     22.0
10 member        Friday         462853     12.6
11 casual        Saturday       499918     26.2
12 member        Saturday       444409     14.3
13 casual        Sunday         428742     27.2
14 member        Sunday         395924     14.3
```

5. **VISUALIZE**
________________________________________________________________________________________________________________

Let us take a look at the visualizations for the dataset.
```
Cyc_bikefinal %>%    #total rides broken down by weekday

group_by(customer_type, weekday) %>% 
  summarise(number_of_rides = n() ) %>% 
  arrange(customer_type, weekday) %>% 
  ggplot(aes(x = weekday, y = number_of_rides, fill = customer_type)) + geom_col(position = "dodge") + 
  labs(x= 'Day of Week', y='Total Number of Rides', title='Rides per Day of Week', fill = 'Type of Membership') +
  scale_y_continuous(breaks = c(250000, 400000, 550000), labels = c("250K", "400K", "550K"))

## `summarise()` has grouped output by 'customer_type'. You can override using the `.groups` argument.
```

The rides per day of the week show casual riders peak on Saturday and Sunday while members peak Monday through Friday. This indicates members mainly use the bikes for their commutes and not leisure.

```
cyc_bikefinal %>%   #total rides broken down by month
  
group_by(customer_type, month) %>%  
  summarise(total_rides = n(),`average_duration_(mins)` = mean(ride_length)) %>% 
  arrange(customer_type) %>% 
  ggplot(aes(x=month, y=total_rides, fill = customer_type)) + geom_col(position = "dodge") + 
  labs(x= "Month", y= "Total Number of Rides", title = "Rides per Month", fill = "Type of Membership") + 
  scale_y_continuous(breaks = c(100000, 200000, 300000, 400000), labels = c("100K", "200K", "300K", "400K")) + theme(axis.text.x = element_text(angle = 45))

## `summarise()` has grouped output by 'customer_type'. You can override using the `.groups` argument.
```

The summer months bring more riders in total but casual rider usage is nearly nonexistent in the winter months. There are multiple factors that contribute to this result but annual members still use the service at a good rate in those months.

```
cyc_bikefinal %>%   #Average length by Customer Type and Day of Week
  group_by(customer_type, weekday) %>% 
  summarise(average_ride_length = mean(ride_length)) %>% 
  ggplot(aes(x=weekday, y = average_ride_length, fill = customer_type))+
  geom_col(position = "dodge") + labs (x="Day of Week", y="Average Ride Length(min)", 
                                      title = "Average Ride Length by Customer Type and Day of Week", 
                                      fill = "Type of Membership") 

## `summarise()` has grouped output by 'customer_type'. You can override using the `.groups` argument.
```

The average ride length of casual riders is considerably longer than that of members and peaks on Saturday and Sunday. Annual members bike a near-constant length regardless of the day of the week.

```
cyc_bikefinal %>%  #Average ride length by customer type and month
 
 group_by(customer_type, month) %>% 
  summarise(average_ride_length = mean(ride_length)) %>% 
  ggplot(aes(x=month, y = average_ride_length, fill = customer_type))+ 
  geom_col(position = "dodge") +
  labs (x="Month", y = "Average Ride Length(min)", title = "Average Ride Length by Customer Type and Month", 
        fill = "Type of Membership") + theme(axis.text.x = element_text(angle = 45))

## `summarise()` has grouped output by 'customer_type'. You can override using the `.groups` argument.
```

The average ride length by casual riders is still considerably longer than members even broken by month. While this would confirm the average ride length by day of the week, it nearly contradicts the rides per month.

```
bike_data1 %>%    #looking at the breakdown of bike types rented
 
  ggplot(aes(x = bike_type, fill = customer_type)) + geom_bar(position = "dodge") + 
  labs(x= 'Bike Type', y='Number of Rentals', title='Bike Type Breakdown', fill = 'Type of Membership') +
  scale_y_continuous(breaks = c(500000, 1000000, 1500000), labels = c("500K", "1Mil", "1.5Mil"))
```

The bike type breakdown shows members use classic bikes much more than casual members. The electric bike use is nearly identical but casual riders are more willing to use docked bikes.

```
cyc_bikefinal %>%     #Looking at demand over a 24 hour day
  
group_by(customer_type, time) %>% 
  summarise(total_rides = n()) %>% 
  ggplot(aes(x=time, y=total_rides, color = customer_type, group = customer_type)) +
  geom_line() + scale_x_datetime(date_breaks = "1 hour",
                                 date_labels = "%H:%M", expand = c(0,0)) +
  theme(axis.text.x = element_text(angle = 45)) +
  labs(title ="Demand Throughout the Day", x = "Time", y = "Total Rides")

## `summarise()` has grouped output by 'customer_type'. You can override using the `.groups` argument.
```

Bike demand over 24 hours reveals that annual members predominantly utilize bikes during rush hours, suggesting a significant portion of them rely on bikes for their daily commute, particularly to and from work. This is evident in the pronounced surge during peak hours, followed by a sharp decline post-5 pm. In contrast, casual riders exhibit a more stable pattern, steadily increasing throughout the day and gradually decreasing after the 5 pm peak.

6. **SHARE**
________________________________________________________________________________________________________________

The data from the above analysis with the visualizations and presentations can be shared based on who is a primary stakeholder or a secondary stakeholder. The kind of information available will depend on the type of team being presented with the insights.

7. **ACT**
________________________________________________________________________________________________________________

A. What are the key takeaways from the above analysis?

• On average, casual riders cover approximately 50% more distance compared to members.
• Annual members predominantly utilize bikes for their daily commutes, with peak usage occurring on weekdays during rush hours.
• The usage pattern of casual riders indicates a preference for leisure, particularly evident in heightened bike usage during summer months and weekends.
• During winter months, casual riders tend to decrease their service usage compared to annual members.
• Classic bikes are the primary choice for annual members, while casual riders are more open to using various bike types.

B. What are some recommendations for the above analysis?

• Implement winter-specific promotions to encourage annual membership sign-ups and convert casual riders to long-term members.
• Reduce the prices of single-fare and full-day passes from Monday to Friday to boost casual ridership on workdays.
• Consider increasing the prices of single-fare and full-day passes on weekends (Saturday and Sunday) to motivate customers to transition from casual ridership to annual membership.

**END OF CASE STUDY**
