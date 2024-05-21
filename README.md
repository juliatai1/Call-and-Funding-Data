# Call-and-Funding-Data
Author: Julia Tai
Date: May 21, 2024

## Description
This project analyzes and compares financial reports and call volume data for cahoots, police, ems and fire. Primarily touching on EDA techniques, figures and statistical tests record how different capacity changes and funding have impacted cahoots’ and other agencies efficiency.

# Research Questions
How have the proportion of calls handled by different agencies changed over time? Has this proportion been affected by increases in cahoots capacity or differences in funding for each agency?

## Data sets used and cleaned
Cad Data (unavailable to public): 
- 18 columns:
  'Call_Created_Time': call created time, type = datetime object 
  'PrimaryUnitCallSign': primary unit call sign, values = "cahoots", "other agency"
  'Disposition': disposition/type of call, sorted by calls implying an angency responded, showed up to an event and performed an action

Financial data: 
- Police, EMS, Fire Annual Funding: Used the expense values from the city annual financial for 2016-2021. Note: the total funding value, therefore did not include annual grant or donation amounts. Source: https://www.eugene-or.gov/107/Financial-Reports
- Cahoots Annual Funding: Used the revenue total per year from 2016-2021. Note: this includes all grant and donation amounts. Source: https://projects.propublica.org/nonprofits/organizations/930585814 
