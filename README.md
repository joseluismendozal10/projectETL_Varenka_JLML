# projectETL_Varenka_JLML

FINAL REPORT 

EXTRACT 1
This analysis uses 3 information sources:
TOP 11 CITIES LIST
The most populated cities in 2019 was extracted from http://worldpopulationreview.com/world-cities/ by reading the HTML table presented there and obtaining the first 11 cities with its 2019 and 2018 population and Yearly change.
a.	We extracted 11 cities, because “Osaka” is not included in the Temperature file and we did not find if there is an alternative name for it.

TEMPERATURE RECORDS DATA FRAME
The recorded temperatures up to the year 2013 for each city were extracted from the file GlobalLandTemperaturesByMajorCity.csv (retrieved from https://www.kaggle.com/berkeleyearth/climate-change-earth-surface-temperature-data )The information was uploaded to Pyhton by using pandas. This table has the following Columns:
1.	dt: year-month-day of the record
2.	AverageTemperature
3.	AverageTemperatureUncertainty
4.	City
5.	Country
6.	Latitutde
7.	Longitude

TRANSFORM
Matching Cities’ names
Some cities are called differently in the information sources, so we had to see how they are included in the PopulationStat webpage in order to assure the information of the population trend was extracted. The changes were:
1.	In the Top 11 Cities List, “Mumbai” (India) to “Bombay”
2.	In the Temperature Records Data Frame, “Mexico” to “Mexico City”, “São Paulo” to “Sao Paulo” and “Peking” to “Beijing”
3.	For the extraction of the Population History a middle dash (“-“) replaced the spaces in “Mexico City” and “Sao Paulo”
Temperature records for the Top 10 Most Populated Cities
1.	From the dt column, the year was extracted into a new column named “Year”
2.	The table of Temperature records was cut to present only the temperature records after 1950 (inclusive) and the cities included in the Top 11 Cities List.
a.	At this point “Osaka” will be removed, since it is not included (as “Osaka” at least) in the Temperatures file.
3.	The Yearly Temperature Average was calculated for each city (from 1950 to 2013)
4.	The Data Frame was ordered by Year from the oldest to the most recent.
5.	The first 10 lines from the Yearly Temperature Data Frame were extracted in order to have a smaller table from where we could extract the information of the country to which each city belongs.

EXTRACT 2
POPULATION HISTORY 
The population since 1950 was obtained by scrapping the following web site https://populationstat.com/ and specifying the country and city in order to obtain individual information for each city needed. For example: https://populationstat.com/Japan/Tokyo
1.	This was done with a FOR loop based on the Top 10 cities list:
a.	From the cities list, we searched for the first city, then in the Yearly Temperature Data Frame (first 10 lines) we searched for the country by filtering the city, we added then the country and city names to the initial PopulationStat url and extract the population information by scrapping the table where the population from 1950 is. This was done by scrapping. Once the reading of the population table is finished, the information is uploaded to a new Data Frame (city population) which then will be appended to the main population Data Frame (cities population)
TRANSFORM
Joining Tables
Once the Population History process concluded, the Temperature Data Frame and the Cities Population Data Frame are joined based on the city and the year.
Creating Graphs
Graphs where created with both measures (Temperature and Population) for each city.
LOAD
The final Data Frame was uploaded into SQL. This Data Frame includes the following information for the 10 cities and from 1950 to 2013 years:
1.	Year
2.	City
3.	Country
4.	Average Temperature
5.	Average Temperature Uncertainty
6.	Population
