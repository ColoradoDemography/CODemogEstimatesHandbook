# Residential Construction Survey


## Goal and Timing

The Residential Construction Survey is run yearly, typically during November or December, to collect data on housing unit change at the municipal-level for the next estimates year. We need to the housing unit data to use the housing unit method for estimating population at these levels.  Data on building permits, certificates of occupancy, demolition permits (or housing loss), and mobile home change are collected according to the definitions below.

While we've typically launched the survey at the beginning of December, due to the Census moving their date for housing unit review in their process forward, this process should by in the field by the week after the Annual Meeting, the first Friday in November.  

## Data Collected

The RCS collects data on building permits, certificates of occupancy, demolition permits (housing loss), and mobile home change.  We do so following specific definitions and timing to adhere to the estimates methodology and to the Census review requirements.  While the timing below represent the specific definitions, we need a consistent time-series from 2011 forward for inclusion in the estimates.

### Building Permits

The data needed to track building permits are the number of permitted residential **units** by month.  These are not to include additions, roofs, etc. that do not result in the creation of a new living unit.  It's important that this definition is adhered to, as we often find under counting of multi-family units and overcounting of new units due to these issues.  

Building permits are issued at the beginning of the construction process, therefore, we assume a 6 month lag between issuance and completion.  This means the for the July 1, 2017 estimates, we use calendar year 2016 building permits.  We will accept data more recent than that, but it won't be included in the estimates process.

### Certificates of Occupancy

The data for certificates of occupancy is similar to building permits, but represents the number of completed **units** by month. These are only to include residential units, not commercial.  We get far fewer submissions of these, but the submissions we do get are typically correct.

Certificates of occupancy are issued once the unit is considered habitable by the permitting entity. As such, we assume that they are immediately available and in the housing stock with no lag.  So for a July 1, 2017 estimate, we require certificates of occupancy from July 1, 2016 to June 30, 2017 by month.  

### Demolition Permits 

The data for demolition permits are designed to represent a way to track housing unit loss.  This could be due to actual demolition, natural disaster, etc.  We asked for the number of demolished **units** by month and while this isn't a hard and fast rule we require a demolition permit to be referenced.  Demolition permits are tricky.  First, not everywhere issues them.  Second, some places offer building and demolition permits in one for scrape and rebuild projects, meaning we need to be careful about how we collect them to avoid double counting.

As for timing, we use the same assumption as certificates of occupancy, that as soon as a demolition permit is issued, the housing unit is lost to the housing stock.  For a July 1, 2017 estimate, we require demolition permits from July 1, 2016 to June 30, 2017 by month.

## Contacts

The contacts we use for this process are kept in MailChimp as a base, but also updated in LGIS (LINK HERE which can also be gotten from anyone on Scott's team) under the Demog contact type.  The RCS Contact type in MailChimp is the base, but when we get a bounce, we replace it with the CTF Administrator contact from LGIS.  That helps ensure we get an email to someone at the municipality. Elizabeth can access the email list and previous emails through the MailChimp account. 

The RCS Contact list is distinct because typically we are asked to talk to a building department employee or director rather than a finance manager (which is typically who the CTF Administrator is).  It's a bit tedious to keep the email list in two places, but it will help in the long run.  

## Data Presented - R App

Communities are also able to view the prior vintage of estimates, including data from the Census and prior construction data during the RCS.  This helps in providing corrections of previous submissions and provides an opportunity for feedback.



The data that we load into the R application comes from the Table 2 Report Selector in the Estimates Database and the construction data masters. This selector needs to be updated every time you add a year of data, but that is done for the previous year's CTF Challenge, so it is always ready for the RCS.

The last year, we displayed that in the Shiny app located at J:\Estimates\Admin\AppDevelopment\rcs_data.  The app can be viewed at https://gis.dola.colorado.gov/app/rcs_data. 



Previously, the data had been displayed in Table 2, which can be seen J:\Estimates\Admin\Websites\v2015ResidentialConstructionSurveyWebsite. That will give you a couple ideas of how we've done it  before.

## Handling Responses

The responses are gathered through a Google Form (located here:https://docs.google.com/a/state.co.us/forms/d/1YgVCqIEYtZe110lYNdYio3KX78JwDTx2Z38z57yCXlg/edit).  Spreadsheets (J:\Estimates\Admin\Websites\v2016ResidentialConstructionSurveyWebsite) were then posted to the RCS site and entities would download and fill them out.  These spreadsheets were uploaded using a page generated by the following Google Scripts: 

Construction Data: https://drive.google.com/open?id=1CWdQRW4DRaEYfHAvxR2g7CgIwtuMO9SjycSstS7q5CbjWuWW4D6xtfa7

Group Quarters: https://drive.google.com/open?id=1SH9iom6iu_9NSMtSw7r0_ywT7W5swZ31zDxzN1dsY4VQ0Py6d5v2-Ivc.

After this, the spreadsheets are dumped into a Google Drive folder and processed into a spreadsheet that is created by Todd.  After that, they are pulled into R to be incorporated into the master for each data type.  A noted improvement in this process would be using a validated drop down in the Excel sheets to standardize the names of the communities.

### R Script

This section will describe the logic that drives the scripts in the J:\Estimates\ConstructionData\LocalUpdateData\v2016\MasterCreation\.  

The processed data sit in seperate spreadsheets for each type of data, just like the previous masters.  All new data and previous masters are loaded into R for comparison.

A crosswalk is manually created (this could be automated if data is better validated) to match each area name with the appropriate county and place FIPS for joining. 

After that, each data set is taken from wide to long.  Each row is identified by the county, place, year, and month.  The Master is merged with the new data in separate columns.  Then you compare the permit data in each row, for inclusion in the master.  Generally, we take the new data over the old data, unless anything look suspicious or like an error.  The script assumes that the input data has either been corrected or is right, it takes new data to either revise or add to data in the previous master.  Then the data is summed to the proper annual or fiscal totals for inclusion in the Estimates Master, added to the monthly data, and exported to a csv.



### Master Spreadsheet.

Once all of the masters are exported to csv files, then you need to add them to the Master Spreadsheets linked into the Estimates Database.  

To do this, create a new sheet in each spreadsheet labeled with the new vintage (e.g. v2017), then import the csv for that Master.  Repeat this for each type of data and have the Estimates Demographer re-link the data to the new sheet.