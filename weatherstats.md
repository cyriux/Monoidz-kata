# Let's talk about Weather!

There are weather stations spread all over the world. Not all weather station record every kind of weather measurement: for example some record only temperature and precipitations, other record humidity and barometric pressure, and some only measure air quality. As opposed to “partial observations”, “full observations” record every possible weather measurement.

When a station does not provide all data, it must be merged with another nearby station to provide a full set of weather stats reports.

From observations we want to produce *weather stats reports* over geographical areas (region, country, continent) and over periods of time. 

Weather stations compute the weather stats reports according to their importance: local stations only deals with their own data, while national stations compute stats from all other stations from the same country. Continental stations produce the reports from all the country reports.

Wa want to produce these stats on-demand, in real-time, and over a large historical time ranges. And we want to be LAZY as developers!

# Your work

Using TDD, the following tests progression is suggested:

1. A weather stats report (temperature, humidity) is equal to itself
1. A single weather stats (temperature, humidity) observation is equal to its average
1. Average of two weather stats report (temperature, humidity)
1. Average of three stats reports (temperature, humidity)
1. Average of stats reports (temperature, humidity, precipitations)
1. Average over 3 weeks is the average of a 2-weeks average and a 1-week average
1. Average of stats reports with some missing measurements
1. Add standard deviation of temperature
