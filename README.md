# BESCOM Twitter Complains
### A project aimed at bringing awareness towards repeated power cuts. 

Power cuts in Bangalore happen for many reasons.
- Rain
- Scheduled maintenance downtime
- Overload
- Load shedding

The goal is to understand which of the reasons causes majority power cuts. 

### Initial Hypothesis

As someone who has lived in Bangalore for over 6 years, here are some things i have observed over a period of time: 

1. Scheduled maintenance causes 10% or less power cuts per month (depending on the area, if there is a maintenance planned, else the value for this factor would be 0%).
2. Less then 40% power cuts in a month are the result of rain.
3. Rest of the power cuts are due to Load shedding or Overload in subdivisions due to bad infrastructure. 

### Data Sources

1. Twitter for user complains.
2. BESCOM's site for monthly maintenance schedules.
3. OpenWeather API for historic montly data.

### Tweet Analysis

1. Tweet can contain only insults or sarcasm and no location.
2. Tweets can contain sarcasm and location.
3. Tweets can contain only pincode.
4. Tweets can contain only location (correct spelling).
5. Tweets can contain only location (incorrect spelling).
6. Tweets can contain location(incorrect spelling) and pincode.
7. Tweets can contain location(correct spelling) and pincode.
8. Tweets can contain only appreciation.
9. Tweets in local language, Kannada.

- Point 1 and 8 are of no use to us. 
- Point 3, did not visit in stage 1 analysis
- Point 6 & 7, partly covered in stage 1 analysis (no Pincode analysis)
- Point 9, did not visit in stage 1 analysis


## The Process
### Project would be divided in 2 stages: Stage 1 | Stage 2 (not done yet)
This is because to source data for scheduled downtime, BESCOM only provides monthly excel files. The older months data is deleted from public eye. Hence we can do October months Analysis once October ends. This is because we need to wait for the month to end to scrape tweets from twitter.

### Stage 1

To understand which areas have been the most affected (extracted from complains on twitter), i webscrapped data from 01/01/2022 until 30/09/2022. (you can find the cleaned data with just locations,date and time in the repo)

The process here is straight forward. I took down all the localities of bangalore and made a list out of them. Then we itterate through the tweets till we extract our locations. 
Create an aggregate of all the locations and plot them in a visual. 

![image](https://user-images.githubusercontent.com/6307592/197025070-6d4f8a1f-7cfc-4c0f-b1a9-1235efe7782a.png)

The problem with my current approach is that it uses partial string matching so i had to re arrange few location name in the list so it would correctly extract the locations. After some manipulation, i achieved 90% accuracy.

I then created 2 datasets, one raw, and the other grouped. 
- Grouped: locations with similar names like 'Koramangala 5th Block', 'Koramangala 8th Block' are now both under the alias 'Koramangala'.Not only this, but also smaller localities falling within bigger locations are grouped under the parent.
- Raw contains locations name as written by users on twitter. 

Note: Also cleaned up any typos/incorrect spellings directly in excel. This is captured in the grouped dataset.

Tableau Dashboard: [Grouped](https://public.tableau.com/views/NammaBESCOMComplainsOverviewGrouped/Dashboard1?:language=en-US&:display_count=n&:origin=viz_share_link) | [Raw](https://public.tableau.com/views/NammaBESCOMComplainsOverviewRaw/Dashboard1?:language=en-US&:display_count=n&:origin=viz_share_link)

Findings from Stage 1:

1. Locations with very high population also resulted in many more complains on twitter.
2. Just because one location as less complains does not mean it has less power cuts, but rather fewer people live in such locations to complain on twitter or are unaware of BESCOM's presence on twitter or do not use twitter.


### Stage 2

WORK IN PROGRESS


# Improvements
1. Use NLP and create a custom model to capture local locations.
2. Ability to capture pincode and map to a location.
3. Create pincode attribute in CSV and load in Tableau/Power BI to create a heat map of Bangalore City
