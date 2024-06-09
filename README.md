# Call and Funding Data
Author: Julia Tai

Date: May 21, 2024

## Description
This project analyzes and compares financial reports and call volume data for cahoots and police. It primarily touches on EDA techniques, while figures and statistical tests record how different capacity changes and funding have impacted cahoots’ and other agencies efficiency.

## Research Questions
How have the proportion of calls handled by different agencies changed over time? Has this proportion been affected by increases in cahoots capacity or differences in funding for each agency? 

The questions I have posed get at the heart of cahoots’ mission statement and their efforts to provide a more equitable and community/client focused alternative to the police. By analyzing calls in parallel with funding, I can create a data driven story about the relationship between cahoots and police.

## Data sets used and cleaned

**Cleaning Script:** cleans/formats and creates all necessary data (CAD and Financial).

Relevant packages: pandas, numpy, datetime

**Final dataframes used in Analysis Script:**
  
Cad Data: 

monthly_calls dataframe: 
- 3 Columns:
  
  Column 1: 'PrimaryUnitCallSign' = primary unit call sign, values = "Cahoots", "Police", type = string object
  
  Column 2: 'Year_Month' = granularity of the dataframe is month, dates = 2016-01-01 to 2020-12-01, type = string object

  Column 3: 'Call_Volume' = total call volume for the agency that month, type = integer

daily_calls dataframe:
- 3 Columns:

  Column 1: 'PrimaryUnitCallSign' = primary unit call sign, values = "Cahoots", "Police", type = string object
  
  Column 2: 'Year_Month' = granularity of the dataframe is month, dates = 2016-01-01 to 2020-12-31, type = string object

  Column 3: 'Call_Volume' = total call volume for the agency that month, type = integer
  

finance_data dataframe:
- 5 columns:
  
  Column 1: 'Year' = year (2016 - 2020), type: integer
  
  Column 2: 'Agency' = agency ('White Bird' or 'Police'), type: string

  Column 3: 'Funding' = annual Funding, type: float

  Column 4: 'Call_Volume' = Total number of calls for the year, type = integer

  Column 5: 'Call_Per_Funding' = Number of calls answered per dollar of funding, type = float
  
- Police Annual Funding: Used the expense values from the city annual financial for 2016-2022. Note: the total funding value, therefore did not include annual grant or donation amounts.
Source: https://www.eugene-or.gov/107/Financial-Reports

- Cahoots Annual Funding: Used the revenue total per year from 2016-2022. Note: this includes all grant and donation amounts. Cahoots is an extension of White Bird. Considering other agencies have additional operational functions beyond responding to calls, funding reflected White Bird and not just the amount allocated to Cahoots. This made comparing other agencies and White Bird funding more realistic.
Source: https://projects.propublica.org/nonprofits/organizations/930585814

## Analytical Steps
Visuals and Statistics:
1.	Load Data: cleaned cad data (new_call), monthly call data (monthly_calls), daily call data (daily_call), financial data (finance_merged)
2.	Annual Funding:
   
•	Input: finance_data

•	Output: bar plot using matplot and seaborn

4.	Call Volume: line graph using matplot, records the total number of calls through time, a vertical line is placed where there is an addition of a new van
   
•	Input: monthly_calls

•	Output: line graph using matplot, records the total number of calls through time, a vertical line is placed where there is an addition of a new van

6.	Average Number of Calls per Dollar of Funding:
   
•	Input: new_call

•	Output: bar plot using matplot and seaborn, primary graph in comparing the efficiencies of Police and White Bird

8.	P-values:
   
•	Input: daily_calls, average daily call volume one year before and after the event

•	Output: p-values for Police + Cahoots, Police, and Cahoots. Used the scipy.stats package

10.	Z-score:
    
•	Inputs for the function:

  •	 x1 = number of successes or events of interest in the first group
  
  •	n1 = total number of trials/observations in the first group
  
  •	x2 = number of success/events of interest in the second group
  
  •	n2 = total number of trials/observations in the second group
  
•	Input: daily_calls (for cahoots)

•	Output: z-score, determines if the proportion of calls before and after the event were significantly different

Relevant packages: pandas, numpy, scipy.stats, statistics, seaborn, matplotlib.pyplot, matplotlib.dates

