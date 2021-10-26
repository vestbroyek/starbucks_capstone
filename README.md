# Starbucks project README

## Project overview

This project is about understanding how offers sent by Starbucks to customers impact their behaviour. We are particularly interested in understanding how different offer types influence people depending on their demographic. 

## Data
We have been provided with three main datasets.

- Portfolio
This data contains information about different offer types, how much spend is required to complete the offer, how long it is valid for, how much (if any) the reward is, and which channel it was sent to the customer through.

- Profile
Demographic data, incuding customers' age, when they became a member, gender, and income.

- Transcript
Records of events, such as offers received, viewed, and completed as well as transactions for each person and the time at which the event occurred.

## Problem statement
There are three interrelated problems this project seeks to answer.

- In general, how do customers who are likely to be incentivised by offers differ from other customers?
- How do we conceptualise who is actually a 'successful' customer, not just likely to be incentivised?
- Are there differences in terms of which type of person responds to which offer?
- Can we use these differences to identify new customer opportunities? 

In other words, the aim of the project is to identify people who have responded to offers in the past and use that information to try to identify new customers who have not yet been targeted.

## Strategy
To achieve the goals discussed above, I will take the following steps.
#### Step 1
Create a joint dataframe to display transactions, demographic, and offer data together. This will involve some data cleaning (extracting data from columns such as 'value') as well as a bit of feature engineering, such as number of transactions, average spend per transactions, etc. in order to get as much information as possible. This will be stored in a 'master' dataframe. I will also produce a 'demographic' dataframe containing information about customers (one customer per row), including the additional features I created, and an 'offers' dataframe.
#### Step 2: Approach
From this, I can begin to answer the first question: what is the profile of people likely to be incentivised by offers. I will define this group as those who have viewed at least one offer, completed at least one, and who don't spend more than \$20 per transaction. Once I have dropped the rows that don't meet these criteria, I can group by person to get dataframes of people who are and aren't likely to be incentivised. I will use this data to explore their demographic characteristics. 
#### Step 2: Expected solution
I expect to see that people likely to be incentivised by offers will have lower incomes, which will likely correlate with them being younger, and lower spend per transaction. I don't think there will be a significant gender component to this.

#### Step 3: Approach
Once we have developed a picture of the people likely to respond to offers in general, it is time to zoom in and answer the core question: per offer type, which demographic should Starbucks target? 

For this, I will subset all the data about offers into an 'offers' dataframe from the master dataframe. I will need to do a bit of cleaning in order to capture what offer type the event relates to (bogo / discount / informational, reward, difficulty etc.) as well as separate information individually about reward value, difficulty and so on. Moreover, where necessary (such as gender) I will convert categorical values into dummy columns in order to enable analysis.

Next, I will only focus on the people I have identified as being likely to respond to offers - meaning they have viewed and completed at least one offer, i.e. they have actively engaged with the programme at least once, and don't spend so much per transaction that they would complete any offer anyway. 

I can then group the offers and see the demographic information about each group. This can be a useful first way to build intuition about how people who engage with individual offers differ from other customers. 

After that, I will dig deeper into what constitutes a 'successful' customer beyond just their likelihood to respond to offers. I will take the concept of a customer journey, i.e. the whole process of receiving, viewing, and completing an offer as more solid evidence of the profile of a successful customer per offer type.

I will then be able to identify everyone who has completed one or more full customer journeys per offer. I will use this demographic information to build a function that will create a report, per offer, of how successful customers differ from the rest of the population.

Having then identified which demographic characteristic set successful customers for that offer apart from others, I will create another function that will, based on selected characteristics and a granularity parameter, suggest potential new customers who match the profile but have not yet been targeted.

#### Step 3: Expected solution
I expect that people who have been members for longer will have higher engagement with offers even though they are sent fewer. I also expect that people on lower incomes will be more sensitive to cheaper offers as well as offers with a higher reward / cost ratio. Finally, I expect the penetration of channels to vary by age.

## Metrics
As this is not a machine-learning project, I rely less on metrics and more on business rules of thumb. For example, I define people likely to be incentivised by offers as those who have received, viewed, and completed at least one offer (meaning they know how the programme works), but don't complete more offers than they view (meaning they might mostly 'accidentally' complete offers) and who don't spend so much per transaction that they would complete any offer anyway.

Similarly, I use the logic of customer journeys to really zoom in on successful customers per offer. A customer journey is when an individual customer has received, viewed, and completed a specific offer. Only the end-to-end completion of this journey counts as an individual successful journey.

## Technical details
Libraries used:
- pandas
- numpy
- seaborn
- math
