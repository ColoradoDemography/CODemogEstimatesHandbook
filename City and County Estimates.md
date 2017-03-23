# City and County Estimates

#Outline
1. Input Data
	1. Construction Data and Source Choice
	2. Group Quarters verification
2. Methodology
3. Database Specifics
4. Review Considerations/ Tests
	1. County Sums - Tp Gqp
	2. Non-negative values

# Input Data
Aside from relying on the county estimates as benchmarks, the city and county process is largely dependent on housing and group quarters data.  These two data types are collected using fairly complex methodologies that I felt we best described in their own sections.  The Residential Construction Survey section deals with the details of collecting and processing the construction data needed for this process.  The RCS also asks areas for GQ data.  Additionally, there are prisons and the College Survey to be concerned about.  Looking into the RCS and GQ sections will give you a good idea of what our input data looks like.

#Methodology
#Database Specifics
##Tables
The following tables are relevant and used in the creation of the City and County estimates. Each table is described and any useful details provided.

CityandCounty_Estimates2010_Master: This is the most important table.  It includes the actual estimates and the various components.  Most of the following tables help to update this one.  If you need data on places, come here first.

CityandCounty_AnnualConstructionData_2010: This table is the second most important.  It is used to house all of the construction data and is manually updated to reflect the proper source for each year.  We try to use local data, but if we can't we use Census.  If we ahve a good timeseries, we use Local Building Permits.  We only use COs if we can do so for the whole county.  Census is the back-up for any area we don't have data on.  The source needs to be set for each year.

CensusCityandCountyMaster_2010: This table is not used directly in the estimates process, but is included when we generate the review reports to help communities understand the differences.

CensusHousingUnits_Master_2010: This table contains the Census housing unit estimates which also had building permits.  This file is used to create the CityandCounty_AnnualConstructionData_2010 table.

CityandCountyBoundaryChange_2010: This table contains changes in housing units and population due to annexations or deannexations.  The input data comes from the GIS Analyst, currently Daniel Trone, and the input is a bit non-traditional.  You'll need to add the units to the annexing place and remove them from the unincorporated area.  If there is more than one annexation then you'll need to summ the changes for both places and input that.  We don't store individual annexations here, although we should.

CItyandCounty_Estimate2010_Overwrites: Sometimes we need to force values to change due to challenges or unreasonable forcing due to the raking procedure.  We do this in the overwrites table.  This table doesn't necessarily contain the exact number you want, but rather the values you need to use to generate the proper outcome in the master table.  It is hand updated only for places that need it.  You should always look to see if you'll need to carry forward updates in this table from year to year to ensure that we continue to take their challenges.

CityandCountyGQBase_2010:  This table contains that base population for each county and place within the counties in Colorado.  It included any changes that we've made to the base over the period.  It is used to create the GQ population estimate using the GQ update tables to bring it forward.

LocalBuildingPermitData_2010:  This is a linked spreadsheet that needs to  get relinked each year.  It links to the most recent vintage tab in the J:\Estimates\ConstructionData/LocalUpdatedData/MonthlyBuildingPermitDataMaster_2010.xls.  This data is updated each year as a part of the Residential Construction Survey.

LocalCertificateofOccupancyData_2010:  This is a linked spreadsheet that needs to  get relinked each year.  It links to the most recent vintage tab in the J:\Estimates\ConstructionData/LocalUpdatedData/MonthlyCertificateofOccupancyDataMaster_2010.xls.  This data is updated each year as a part of the Residential Construction Survey.

LocalDemolitionData_2010:  This is a linked spreadsheet that needs to  get relinked each year.  It links to the most recent vintage tab in the J:\Estimates\ConstructionData/LocalUpdatedData/MonthlyDemolitionDataMaster_2010.xls.  This data is updated each year as a part of the Residential Construction Survey.

LocalMobileHomeData_2010:  This is a linked spreadsheet that needs to  get relinked each year.  It links to the most recent vintage tab in the J:\Estimates\ConstructionData/LocalUpdatedData/SemiAnnualMobileHomeChangeData_2010.xls.  This data is updated each year as a part of the Residential Construction Survey.

## Queries
### Annual Construction Data Queries
These are the first queries you need to run to update the CityandCounty_AnnualConstructionData_2010 table.  These need to be run before the City and County Estimates Queries because they are an input. They can be run all at once using the macro: Step02_AnnualConstructionData_Updater. Each query is prefixed with AnnualConstruction2010_, so I'll just be using StepXX for identifying them while I walk through each one.

	1. Step00: This step pulls in the Census permits and completion rates we'll need later in the process.
	2. Step00a: This step changed nulls to 0 to help later queries.
	3. Step00b: This step should be redundant, but isn't.  It forces the completion rate columns to change. Not sure why this is happening.
	4. Step01: This step pulls in all of the local building data from each Master table and the boundary change table.
	5. Step01a: This step is also redundant and should be needed but is.  It sets the building permits again.
	6. Step02: Creates Multi-County Place Sums of all of the newly imported data.
	7. Step03: Pulls the Multi-County Place sums into the Annual Construction master.
	8. This isn't a query, but you'll need to set the Sources for each place by hand according to the rules outlined above.
### City and County Estimates Queries
These are the semi-complicated queries that need to be run to generate the city and county estimates.There is a macro that will run them all called: Step03_CityandCountyEstimatesMaster_Updater. Each query is prefixed with CityandCountyEstimates2010_, so I'll just be using the StepXX to identify them while I walk through each one.

	1. Step00: This query nulls out the entire table to help make sure that we do not accidentally keep old values.
	2. Step01: This is a bit of a special query.  It is build as a module in Visual Basic that will run a set of SQL commands (based on Access Queries) in the order they need to be run without a ton of individual queries.  It builds the total housing unit estimates for each source.
	3. Step02: This query creates PlaceSums (ironically a table of county-level sums) of housing units for all years.
	4. Step03: This query takes the table of county-level sums and places them into the Master table for the county rows.
	5. Step04: This step changes the persons per household and vacancy rate variables for each place back to their 2010 (adjusted) values.  This is to start the model out, these values change later on.
	6. Step05: This is another module that sets fields to their overwrite values in the event that there are overwrite values to set.  Doing this in a module allows us to run them all in one step.  It's a good time to check that you're making sure that you don't need to pull any of the overwrites forward.  I check the Challenges folder and make sure those are still there.
	7. Step06: This query generates the initial household population for each place in the state.
	8. Step07: This query creates county-level sums of the household population.
	9. Step08: This step pulls the county control household population from the County Master.  This is in preparation of ensuring that the sums from the housing unit match for each county.
	10. Step09: This step adjusts the household population estimates to sum to the county controls by applying a rake. A rake is the ratio of the control to the estimates population for each county. This proportionally adjusts each place within the county based on the county rake.
	11. Step10: This query sets the county estimates in the CityandCountyEstimatesMaster_2010 table to match the control totals to ensure consistency.
	12. Step11: This query recreates a table with the new sums of the place-level household populations by county.  We use it to help idenify rounding issues in the next step.
	13. Step12: THis query takes any differences in the control totals and new sums and adjusts pre-determined adjustment areas.  This should usually only be by 1 or maybe 2, check things out if it is adjusting by more.
	14. Step13: This step recalculates the appropriate persons per household, vacancy rates, and occupied household values based on the changes the rake and rounding made to the population.
	15. Step14: This step creates a table with county housing sums.
	16. Step15: This step updates the county-level rows in the CityandCountyMaster_2010 table and updates them to the appropriate housing data.
	17. Step16: This step creates a table of place-level group quarters sums from the facility update list. Table is called: GQPlaceUpdateTable.
	18. Step17: This step sets all of the group quarters populations to their 2010 base.
	19. Step18: This step updates the base number using the GQ change from the GQPlaceUpdateTable.
	20. Step19: This step creates an updated sum of the County level group quarters data called: PlaceGqpSums.
	21. Step20: This query takes the data from the previous step and updates the county rows in the master with the proper group quarters data.
	22. Step21: This step creates the total population fields in the Master by summing the newly generated household population and the group quarters population.
	23. Step22: This step creates the multi-county place sums for all of the non-rate variables. Basically, we need to add all the parts of places in multiple counties together now that they are all correct and update their values.
	24. Step23: The query updates all of the multi-county place total fields using the table we just created.
	25. Step24: This step creates sums for each variable for places that are multi-county and puts them in a table. This step will let us get data into the county-level row for multi-county places.
	26. Step25: This step updates the multi-county totals row with the data from the previous step.
	27. Step26: This step adjusts the vacancy rates and occupied housing units to account for places that go negative on their vacancy rate due to pop change growing faster than our estimated housing unit change.
	28. Step27: This step creates the StateSums table to use to populate the Colorado state row in the master.
	29. Step28: This table updates the Master with the state total data from the previous step.
	30. Step29: This step updates the vacancy rates and initially updates the persons per household.
	27. Step30: This step recalculates the persons per household to ensure that all components in each row produce their estimates.

After you update all of these queries, try running them all at once.  It isn't that helpful if there is an issue, but it's a really fast way to find one.  If all of the queries run, filter the Master on CountyFIPS (filter out the multi county places) and PlaceFIPS (filter out the county totals where PlaceFIPS is equal to 00000).  Then use the Ribbon to turn on Totals on the table if that isn't already enabled.  Set the total populations to a sum total and then check those values against the state totals from the County Estimates.  If these match, you're in good shape.  Re-save the export specifications (click Export on the review queries, click OK on the first box, then click advanced, then click Save As…on the window that pops up and save it as the same name as the ReviewCopyExportMacro has) and send it to the review app by running the Macro.  OR you can do you review how you want and that is cool too.
