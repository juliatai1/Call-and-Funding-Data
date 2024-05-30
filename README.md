# Call-and-Funding-Data
Author: Julia Tai

Date: May 21, 2024

## Description
This project analyzes and compares financial reports and call volume data for cahoots and police. It primarily touches on EDA techniques, while figures and statistical tests record how different capacity changes and funding have impacted cahoots’ and other agencies efficiency.

The data was mostly clean when provided and therefore, the finalizing steps proved simple. In contrast, I have experienced many setbacks with the financial data. The information has not been easy to acquire with little organizational transparency and notable differences in reporting measures between cahoots and police. I used White Bird’s annual audit reports to reflect the financial backing for Cahoots. This also allowed me to draw a comparison between the efficiency of Police and White Bird as both have other operational agendas. Comparing Cahoots and the Police would oversimplify the allocation of resources within the Police agency, as Cahoots’ sole mission is to answer calls. However, I am aware that by comparing Cahoots and Police, this is still a gross generalization of the two organizations missions and operations, but the comparison is more accurate. To determine annual funding, I referenced the ProPublica White Bird Clinic and the City of Eugene’s Financial Reporting websites. I used the annual revenue value, to represent the annual funding for White Bird. This value includes annual government funding, grants, donations, and revenue from program services. Information on police funding was harder to find, and I ended up just using the expense value on the city’s financial reports. Therefore, no other grants, donations, or other values were considered. 

## Research Questions
How have the proportion of calls handled by different agencies changed over time? Has this proportion been affected by increases in cahoots capacity or differences in funding for each agency? 

The questions I have posed get at the heart of cahoots’ mission statement and their efforts to provide a more equitable and community/client focused alternative to the police. By analyzing calls in parallel with funding, I can create a data driven story about the relationship between cahoots and police.

## Data sets used and cleaned

**Cleaning Script:** cleans/formats and creates all necessary data (CAD and Financial).
  Overview of the process: 

Cad Data:
1.	Load CAD data set
2.	Filter to relevant columns: 'Call_Created_Time', 'PrimaryUnitCallSign', 'Disposition'
3.	Filter Disposition: Implies Agency showed up to a call and performed an action or is NA*
4.	Filtered out the years 2021-2022
5.	Convert Call_Created_Time column to datetime object
6.	Convert values of PrimaryUnitCallSign to Police or Cahoot
7.	Send dataframe to CSV file

Call by Time Unit Data: 
1.	Call by year
2.	Call by Month, send to csv
3.	Call by day, send to csv

Financial Data:
1.	Create Cahoots financial dataframe
2.	Create Police financial dataframe
3.	Merge the 2 dataframes
4.	Send merged funding data to csv
5.	Add call volume to the previous dataframe
6.	Add call per dollar funded to the previous dataframe
7.	Send dataframe to csv

Relevant packages: pandas, numpy, datetime


**Final dataframes used in Analysis Script:**
  
Cad Data (unavailable to public): 

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
  
- Police, EMS, Fire Annual Funding: Used the expense values from the city annual financial for 2016-2022. Note: the total funding value, therefore did not include annual grant or donation amounts.
Source: https://www.eugene-or.gov/107/Financial-Reports

- Cahoots Annual Funding: Used the revenue total per year from 2016-2022. Note: this includes all grant and donation amounts. Cahoots is an extension of White Bird. Considering other agencies have additional operational functions beyond responding to calls, funding reflected White Bird and not just the amount allocated to Cahoots. This made comparing other agencies and White Bird funding more realistic.
Source: https://projects.propublica.org/nonprofits/organizations/930585814

## Analytical Steps
Visuals and Statistics:
1.	Load Data: cleaned cad data (new_call), monthly call data (monthly_calls), daily call data (daily_call), financial data (finance_merged)
2.	Annual Funding: 
•	Input: finance_data
•	Output: bar plot using matplot and seaborn
3.	Call Volume: line graph using matplot, records the total number of calls through time, a vertical line is placed where there is an addition of a new van
•	Input: monthly_calls
•	Output: line graph using matplot, records the total number of calls through time, a vertical line is placed where there is an addition of a new van
4.	Average Number of Calls per Dollar of Funding: 
•	Input: new_call
•	Output: bar plot using matplot and seaborn, primary graph in comparing the efficiencies of Police and White Bird
5.	P-values: 
•	Input: daily_calls, average daily call volume one year before and after the event
•	Output: p-values for Police + Cahoots, Police, and Cahoots. Used the scipy.stats package
6.	Z-score:
•	Inputs for the function:
•	x1 = number of successes or events of interest in the first group
•	n1 = total number of trials/observations in the first group
•	x2 = number of success/events of interest in the second group
•	n2 = total number of trials/observations in the second group
•	Input: daily_calls (for cahoots)
•	Output: z-score, determines if the proportion of calls before and after the event were significantly different

Relevant packages: pandas, numpy, scipy.stats, statistics, seaborn, matplotlib.pyplot, matplotlib.dates

(*) = Disposition reasoning

Values implying an agency went to an event, located and performed an action at the incident: 

'ADVISED’ 
'ASSISTED'
'REPORT TAKEN'
'WARNING'
'PATROL CHECK'
'CITED IN LIEU OF CUSTODY'
'SOBRIETY CHECK'
'UNIFORM TRAFFIC CITATION ISSUED'
'NON CRIMINAL HOLD'
'ARREST'
'ASSISTING OFFICER'
'WELFARE CHECK DONE'
'K897 DEPLOYED'
'TRANSPORT MADE'
'FOLLOW UP INVESTIGATION'
'RETURNED TO OWNER'
'FIELD INVESTIGATION'
'VEHICLE TOWED NON IMPOUND'
'PUBLIC WORKS'
'ABANDONED VEHICLE'
'BUILDING CHECKED SECURE'
'CIVIL ISSUE'
'CAMPING COMPLAINT CLOSED FOR PATROL'
'ILLEGAL CAMPING IN A VEHICLE'
'K896 DEPLOYED'
'ILLEGAL CAMPING IN PARK'
'FIX-IT TICKET'
'PARKING CITATION ISSUED'
'DENIED FIREARM SALE'
'UNHOUSED RELATED ISSUE'
'VEHICLE IMPOUNDED',
'TRAFFIC ENFORCEMENT UNIT'
'TAGGED IE PARKING CITE ISSUED'
'PATIENT TRANSPORTED'
'K893 DEPLOYED'
'TRAFFIC STOP ONLY'
'RELAYED TO COTTAGE GROVE DISPATCH'
'REPOSSESSED VEHICLES'
'RELAYED TO JUNCTION CITY DISPATCH'
'JUVENILE TAKEN INTO CUSTODY'
'DAMAGE'
'MEDICAL AID EPD'
'EXECUTIVE ORDER 2012 VIOLATION'
'K898 DEPLOYED'
'ACTION TAKEN'
'K895 DEPLOYED'
'K891 DEPLOYED'
'FIRE NO DAMAGE'
'PERSON STOP ONLY'


Additional explanation:
nan: assuming that the agencies went to the event, located and performed actions at the incident


Values implying an agency did not go to an event, locate, or perform an action at the incident

'UNABLE TO LOCATE'
'GONE ON ARRIVAL'
'DISREGARD'
'INFORMATION ONLY'
'DISREGARDED BY DISPATCH'
'RESOLVED'
'UNFOUNDED'
'WILL CALL BACK'
'NO INVESTIGATION'
'QUALITY OF LIFE - NO DISPATCH'
'QUIET ON ARRIVAL'
'FALSE ALARM'
'ACCIDENTALLY CHOSE NEW EVENT'
'MOTOR VEHICLE ACCIDENT - NO DISPATCH'
'DISREGARDED BY PATROL SUPERVISOR'
'CALLER CALLED BACK
'UNABLE TO DISPATCH'
'MISTAKEN ALARM'
'CANCEL WHILE ENROUTE'
'NO ACTION TAKEN'
'NO PATIENT TRANSPORT'
'CANCELED REPORT NUMBER'
'CANCEL FIRE UNIT FROM CALL'

Additional explanation:
'DEAD ON ARRIVAL': were not able to perform an action
'REFUSED SERVICES': were not able to perform an action

Unclear: not reporting this
'RIGHT OF WAY CAMPING'
'SPX'
'SEND PCR REPORT'
'REFERRED TO OTHER AGENCY': The call was diverted to this agency
'RELAYED TO OREGON STATE POLICE'
'RELAYED TO LANE COUNTY SHERIFFS OFFICE'
'RELAYED TO UNIVERSITY OF OREGON POLICE'
'RELAYED TO PARKING CONTROL'
'RELAYED TO DESCHUTES 911'
'RELAYED TO LINN COUNTY 911'
'RELAYED TO BENTON COUNTY'
