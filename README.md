# Citybike: Rental Behavior Comparison for the Months of April in the Years 2018-2020

(Data Analytics Bootcamp Certificate Tableau Homework - CitiBike)

https://public.tableau.com/views/citibike_homeworkRRG/PercentBikerentalsneartimessquare?:language=en-US&publish=yes&:display_count=n&:origin=viz_share_link


## Chosen Exploration:
Changes in bike rental behavior in the month of April for the years 2018, 2019 and 2020. The purpose of this granularity was to try and visualize the effect the pandemic could have had in the rental habits in NY.

### Data Wrangling/Clean-up:
* 201904-citybike-tripdata, 201804-citybike-tripdata and 2020-citybike-tripdata csv files were downloaded from https://www.citibikenyc.com/system-data.
  * Files were open in a jupyter notebook, changed to dataframe and concatenated together. The new dataframe was exported as a new csv file.
  * New csv file was open in Tableau
* Calculated fields in Tableau
  * Number of bike rentals = count of each entry
  * Distance = 3959 * ACOS (SIN(RADIANS([Start Station Latitude])) * SIN(RADIANS([End Station Latitude])) + COS(RADIANS([Start Station Latitude])) * COS(RADIANS([End Station Latitude])) * COS(RADIANS([End Station Longitude]) - RADIANS([Start Station Longitude])))
    * Formula obtained from: https://kb.tableau.com/articles/howto/calculate-the-distance-between-points-on-a-map
    * Used to determine the distance covered from start station to end station.
  * Diverging gender
    * IF [Gender] = 1 THEN -[Gender] ELSE [Gender] END
    * Used to create diverging bar graph (tree style)
  * Percent Difference # Bike Rentals
    * (ZN([Percent of Total Bike Rentals]) - LOOKUP(ZN([Percent of Total Bike Rentals]), -1)) / ABS(LOOKUP(ZN([Percent of Total Bike Rentals]), -1))
      * Formula from: https://kb.tableau.com/articles/howto/calculating-the-year-over-year-difference-of-the-percent-of-total
  * Percent of Total Bike Rentals
    * SUM([# of Bike Rentals]) / TOTAL(SUM([# of Bike Rentals]))
* Grouping:
  * From all stations in the NY map, select and keep only the stations in general proximity to Times Squares.
    * Done arbitrarily based on how close they looked on the map.

### Visualizations Created:
  * Individual graphs 
    * Weekly Average Trip Duration and of Of Bike Users Per Station:
      * Contents:
        * 2 columns: 
          * Map with average trip duration markers with color and size indicators based on trip duration in seconds.
          * Map with sum of number of bike rentals per start station with color and size indicators based on trip duration in seconds.
    * Sum of Bike rentals over 2018, 2019 and 2020
      * Line graphs, colored for each year, with the changes in the total of bikes rented overall per day.
    * Divergent graph gender comparison per day
      * Bar graph representing the number of rentals per gender for each day of the week.
    * Total Rider per gender for the entire month for each year
      * Bar graph, dual axis percent and number of bile rentals
    * Top 3 Busiest Stations and Busiest Days
      * Bar graphs (stacked for gender) for the top 3 busiest stations showing in descending order the busiest days of the month for that year.
    * Daily riders changes
      * Line graph with daily variation in the total number of riders, by gender, per year.
    * Daily distance
      * Line graph with daily variation in the average distance of riders, by gender, per year.
    * Top 10 overall busiest start stations
      * Bar graph with number of bike rentals per station divided by gender with dual axis to show the avg distance from bikes from this location.
    * Changes in sum of bike rides from previous year
    * Map Top 10 busiest start stations
      * Ranked in ascending order (color coded) and placed on map based on latitude/longitude of station. Marker size is based on the sum of bike riders. One map per year.
  * Dashboards
    * Bike rental comparison for April 2018, 2019 and 2020
      * Top line graph shows the daily change of the total bike rentals per start station color coded for years
      * Bottom map shows the weekly change in average trip duration and the total number of bike users. Maps should be animated cycling through the different weeks to show the changes.
    * Gender grouped comparison of the average distance and total number of nike rental per start station for the month of April.
      * Top line graph shows variation of daily average distance covered by riders in the month of April for 2018, 2019 and 2020.
      * Middle bar graph shows the overall percentage of total bike riders in April per year. (Actions should automatically change the graph for the appropriate year based on hovering on the top like graph for that year).
    * Change in Bike rides from previous year and percent total bike rental for stations near Times Square
    * Location and ranking of the top 10 most used start stations and name and popular day in April for the top 3 busiest stations for bike rental.
  * Story
     * Story incorporates all of the dashboards and one individual visualizations (comparison of bike rental behavior -# of bike rentals and avg distance) for the month of April in all years selected by gender for the overall top 10 most used start stations.

## Conclusions from the data:
* Daily bike rental was down every day in the month of April in 2020 compared to 2019, as expected given the effect the COVID-19 lockdowns had in NYC. However, for certain days in the month of April in 2020 the total usage per day per starting station was higher than in 2018 and almost on par with 2019. Although bike rental was lower in 2020, it appears trip duration was generally higher.
* Daily average distance traveled by users did not appear to vary too much among genders during the month of April during any of the years selected. There were certain days in 2020 with higher peaks in daily average distance for all genders (April 19 and April=> ~1.5 km) as well as a low point on April 13 with ~1 km as the average distance covered. There is also more usage in general from people identifying as males and that percentage remained in the 60% range regardless of the year the data from the month of April came.
* Looking only at stations selected to be near Times Squares, there was a marked decreased usage of bikes from April 2020 compared to April 2019 which saw an increase in use from 2018. Curiously, there was more of an increase in the average distance covered by riders in these stations. Broken down as percent of total bike rental by gender for the month of April for each year analyzed, there seems to be a minor increase in the percentage of users that identify as female nonetheless, the biggest gender group of users continues to be males.
* The ranked top 10 stations based on number of users remained very similar in 2018 and 2019, but 2020 saw other stations becoming more utilized particularly outside of Manhattan. Also, in the top 3 most popular stations, there was a significant drop of users in all gender groups for the year 2020.
