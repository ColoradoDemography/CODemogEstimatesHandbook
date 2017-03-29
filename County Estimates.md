# County Estimates

# Outline
1. Input Data
2. Methodology
3. Database Specifics
 b. Queries
 c. Tables

## Input Data
### Births and Deaths
One of the core data sources for our estimates come from the Colorado Department of Public Health and Environment (CDPHE), the birth and death data by county.  Our current and longstanding contact is Kirk Bol (kirk.bol@state.co.us) and we get draft numbers around the end of January and beginning of February.  Typically, we get an excel with the sums for each county and variable, but recently, we've been getting microdata (one row per death, one row per birth).  I've been using R scripts to process the data (see the VitalRecordsData>DPHE>2015 folder for an example), but you could also easily use Access or anotherr database to do so.  The main catch is that the file delimits columns using the "|" rather than a "," or tab.  This data does not change once final, so we do not currently vintage the input table.  We need to generate a column of births and one for deaths that span July 1 of the previous year to June 30 of the estimate year. 

Once you process the data into two columns, we need to add that to the existing birth and death master files.  These files can be found here: J:\Estimates\VitalRecordsData\DPHE\DetailedTables.  Birthbycounty_master.xls and DeathbyCounty_master.xls.  To do this, first ensure that each dataset is sorted the right way.  Check that Elbert and El Paso and La Plata and Lake are in the same spots, their FIPS codes differ from how most programs sort alphabetically.  Once you have that checked, copy paste the data into the Excel sheet under the proper column (for vintage 2015 I put births in the B1415 column). The data is already linked to the database (assuming you made a copy before you made everything local and archived the last vintage).  

### Net Migration
We get our net migration estimates from the U.S. Census Bureau through our FSCPE partnership.  I will use the review file as default when we get that, but if a detailed final is released before we need ours done, I can use that as well. We use their Net Domestic and Net International estimates summed and subtract out the Census estimated GQ change.  This is done because the Net Domestic Migration column includes GQ change.  We use our own estimates for that, so we subtract it out.  

The data is housed here: J:\Estimates\CensusEstimatesData\CensusCountyMaster_2010.xlsx.  This file is a vintaged (using tabs for each vintage) single source for the most recent review and final Census County Estimates.  The tabs have a year and a letter on the end, either 'r' for review of 'f' for final.  Keep this convention moving forward.  The linked table in the database needs to be relinked to the appropriate sheet every year.

### Group Quarters data
The Group Quarters data lives in a separate database, with it's own set of instructions.  What is key is making sure we've got the proper linked tables.  The EstimatesGQMaster_2010 table is the most important.  Tracing errors always go back to that table for the most part.  Ensure that we've followed the documentation for generating that before looking directly at the facility table or aggregation table.  

## Methodology
## Database Specifics
### Tables
The folowing is a list of tables that are relevant to the process and a brief description of what each one contains.  The tables either live in the Estimates Masters group or the Estimates Input Data group. None of the below tables are edited directly in Access:

County_Estimates_Master_2010:  As the name suggests, this is the table that contains the estimates for the counties and the major components.  It is the reference point for all lower-level estimates as well.  This is generally where to go to find the data for requests or projects.

CensusCountyMaster2010: This table is referenced above and contains the Census Bureau estimates for the same vintage as the database is for.  It's used to populate net migration and for comparison purposes.

CityandCounty_BoundaryChange:  This table links to an excel sheet that aggregates changes in population and housing due to annexations or deannexations.  This table is rarely important for counties, but essential for municipalities.

DOLAMigrationAdjustments_2010: This table is more of a historical relic than anything.  We used to use it to adjust Census Estimates that seemed pretty wrong. I've never used it at all, but we did use it to make adjustments in 2010.

DPHEBirthData: This is the table that links to the birth data excel sheet from CDPHE.

DPHEDeathData: This is the table that links to the death data excel sheet from CDPHE.

QCEWEmploymentData: We don't use this directly in the estimates process, but do include it in the review tables (Draft Table 1) as symptomatic data.  Economist helps update it each year.

### Queries
These queries use the tables above to generate the County_Estimates_Master_2010 table.  There is a macro in the Macros group called Step01_CountyEstimatesMaster_Updater that will run all of them in order.  The list below shows them in the order they need to run in.

All of the queries start with CountyEstimates2010_ and are postfixed with a number of descriptor.  I'll be leaving off the prefix for simplicity.

	1. StepGQ: This query creates the GQUpdate_FacTable which contains all of the facilities and aggregations eligible for inclusion in the process. To update add the next year GXX to the query.
	2. Step01: This table updates the main fields of the County_Estimates_Master_2010 table to the relevant input value or to 0 in the case of GQ to prepare it for use later. Make sure to update each of the variables to the latest year to generate the proper estimates.
	3. Step01a: This query creates the net migration column by adding Net Domestic Migration and Net International Migration together and subtracting Census GQ Change. You'll need to add the next year set to make this work.
	4. Step02: This query updates each county for any boundary changes, but we almost never have any you wouldn't have heard of.
	5. Step03: This query sums the facilities in the GQUpdate_FacList to the county level to prepare for use in creating the GQChange columns. Make sure to include the new year.
	6. Step04: This query updated the GQ Change columns in the master table using the table made in the previous step and by subtracting the totals between the relevant years. Again, check that the most recent estimate year is included.
	7. Step05: This sstep takes all of the updated input data and uses it to generate the population totals for each year by summing all relevant columns for each year together.   Make sure to copy the previous year code and paste it in adding the newst year for each variable to the end and changing the name.
	8. Step06: This table creates the StateUpdateTable by summing all of the variables to the state-level.
	9. Step07: This query places the state totals into the County_Estimates_Master_2010 table using the table created in Step6
