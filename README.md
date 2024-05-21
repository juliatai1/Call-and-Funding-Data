# Call-and-Funding-Data
Author: Julia Tai

Date: May 21, 2024

## Description
This project analyzes and compares financial reports and call volume data for cahoots, police, ems and fire. Primarily touching on EDA techniques, figures and statistical tests record how different capacity changes and funding have impacted cahoots’ and other agencies efficiency.

# Research Questions
How have the proportion of calls handled by different agencies changed over time? Has this proportion been affected by increases in cahoots capacity or differences in funding for each agency?

## Data sets used and cleaned
2 seperate scrips:
- cleaning
- analysis
Cad Data (unavailable to public): 
- 18 columns total, 3 columns used:
  
  Column 1: 'Call_Created_Time': call created time, type = datetime object
  
  'PrimaryUnitCallSign': primary unit call sign, values = "Cahoots", "Other Agency"
  
  'Disposition': disposition/type of call, sorted by calls implying an angency responded, showed up to an event, and performed an action

Financial data:
- 3 columns:
  
  'Year': year (2016 - 2022), type: integer
  
  'Agency': agency ('White Bird' or 'Other Agency'), type: string

  'Annual Funding': Annual Funding, type: float
  
- Police, EMS, Fire Annual Funding: Used the expense values from the city annual financial for 2016-2022. Note: the total funding value, therefore did not include annual grant or donation amounts. Source: https://www.eugene-or.gov/107/Financial-Reports
- Cahoots Annual Funding: Used the revenue total per year from 2016-2022. Note: this includes all grant and donation amounts. Cahoots is an extension of White Bird. Considering other agencies have additional operational functions beyond responding to calls, funding reflected White Bird and not just the amount allocated to Cahoots. This made comparing other agencies and White Bird funding more realistic. Source: https://projects.propublica.org/nonprofits/organizations/930585814 
