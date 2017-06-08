# Federal State Cooperative for Population Estimates

# Outline
1. County Estimate Review
 2. Hints and Tips - We aren't ready usually
3. Housing Unit Review
 4. Timing and RCS
 5. Methodology
6. Subcounty Population Review
7. Group Quarters Report(GQR)
 8. General Thoughts and Process
 9. Query Structure (Refer to GQ DB?)
10. Vital Statistics Request
  1. Totals and Verification
  2. Race and Supression Sheet
11. Meetings
 12. Fall
 13. Spring




# Group Quarters Report (GQR)

To complete this process,, ensure that you're following the guidelines sent by the census and download those files to the Group Quarters>DataFromCensus>XXXX folder, where XXXX is the relevant year.

### Queries

GQR20XX_Step01: This query makes the new table for us to populate by building on the last year's table.  This is done to follow the Census methodology, which requires that each year build on the last for them to include the data.



GQR20xx_Step02: This query adds in all of the new facilities since 2014.  If you add a facility to the database, then you'll need to make sure to tag it as a GQR include to get it in there. You'll only need this if there are new facilities.



GQR20xx_Step03: This query updates all of the facilities included in the GQR from last time (See my note about new facilities).



GQR20XX_Step04: This updated the aggregations (Universities) to the most recent data.  It's worth checking this twice since it's been a problem in the past.



### Preparing the Submission File

Make sure to review the documentation for any changes in format or requirements.  Since we don't have more recent data (I will add in Prisons since we get that easily) most of the most recent year cells will be blank.



#### Step 1 

I make a copy of the template file we download from the Census Bureau and rename it with our State then WORKING at the end.  Ensure that you follow the Census naming requirements when doing this, just add WORKING to the end so you don't get confused.  I edit the template file to look like it will need to for submission by deleting out all the template jargon.  Note: you'll need to fix the data validation cells for comment 1 by moving the options way to the right and changing the data validation cells within each comment 1 cell.



#### Step 2

I copy in the table we make using the queries in the Group Quarters database and pasting it into a blank sheet, then I ensure that the fields are in the right order and copy it into the template.  This is the base for starting my work.  I then carry forward all of the populations that need it and fill in missing Facility ID values.



#### Step 3 

Then I go through and carefully add in the Comment 1 field using the data validation fields.  I also carry over previous comments to ensure that they get captured.  This is especially important for a facility like Ft. Lyon. It is really important to check the all the new data you put in is right and that the facilities you carry forward are done the same way as before.  Also, we've had historical issues with the universities being doubled.  Make sure to check for that.



#### Step4

Once you are comfortable with the shape of the submission, follow Census Bureau instructions for review and filing of the request.





# Vital Statistics Request

In the late summer, about a month after the Group Quarters data are submitted, the Census bureau will send out the County Vital Statistics Report for their next vintage.  They ask for two products, the county level births (which are 'required') and the race detail for births (which are optional, but we provide in a typical year).

## Totals and Verification

The total birth and death counts for each year are sent along by Kirk Bol or someone in his unit from CDPHE at the beginning of July.  We can get provisionals before this, but that is when the final births and deaths are ready.  

Total counts for the counties are on a fiscal year basis, so for the year 2012, the counts included births from July 2011 to June 2012.  In general Kirk sends a file with monthly data and calendar year totals that need to be re-aggregated into the fiscal year and then moved the the birth and death master excel files.  This is generally done by the end of the previous Estimates cycle since ours are due in August.  Therefore we can generally just take that data from there and place it into the templates.  This makes things a bit easier for us, we just need to verify the geographic fields and such.

After I put them all in the spreadsheet template provided, I run a few checks on them including summing to the State totals and checking them individually against my Masters.

## Race data


We have generally provided the Census with our race detail from the CDPHE data Kirk sends. They have recently stopped collecting it, but here is how I did it.  It comes in microdata and I used R to process it and turn it into a usable format, but it could be done in Access or other databases. An example is in this folder: J:\Estimates\VitalRecordsData\FSCPESubmissions\2015VintageVitalStatsSubmissions\.  Double click on the R-Project file and it should open in RStudio.  Otherwise just look at the scripts.

After I have done that I put it into a spreadsheets (examples of which live here: J:\Estimates\VitalRecordsData\FSCPESubmissions\2015VintageVitalStatsSubmissions\2014BirthsAdjust).  The spreadsheet helps keep the totals for the State apparent as we change numbers to meet our Supression agreement with the CDPHE.  Per our agreement we are not allowed to send out data where the cell would be a 1 or a 2 without obscuring that even in some way, usually by changing it from a 1 to a 2 and accounting for that in another cell that keeps the totals the same.  The process can take a long time and is fairly tedious, but it garners good will at the Census.  The general policy for sending this along is that we do it when we can, but if other priorities prevent it we don't send it.  There are formula cells across the top that track any changes between race categories and then formula cells to the right of each county, race, and hispanic combination that tracks the county sums.  Basically, everything in the rows and columns needs to add to the unsupressed sums.  The purpose is two-fold: first, the Census needs that property to be true to validate the data, and second, the data wouldn't be truly supressed because someone could track places where changes were made.

Tip 1: Try to minimize the changes between race totals at all times, then at the end use a big county to fix the 1 or 2 that a race group may be off.  I keep track of the race totals the whole time and never let them get above 3.  I also try to vary which bog county I change to make sure that gets distributed evenly.  

Tip 2: I try to make sure I leave the distribution as close as I can to what it really is.  In many places it is impossible or nearly impossible (e.g. a place with 28 White births and 1 American Indian Birth, 1 Asian birth, and 1 Unknown or a place with only 2 births that are also of the same race), but I will default to that if possible.  So I may try to move a releasable total in additional to the 1 or 2 to keep some of the distributional integrity there.


We have generally provided the Census with our race detail from the CDPHE data Kirk sends.  It comes in microdata and I used R to process it and turn it into a usable format, but it could be done in Access or other databases.  After I have done that I put it into a spreadsheets (examples of which live here: J:\Estimates\VitalRecordsData\FSCPESubmissions\2014VintageVitalStatsSubmissions\2013BirthsAdjust).  The spreadsheet helps keep the totals for the State apparent as we change numbers to meet our Supression agreement with the CDPHE.  Per our agreement we are not allowed to send out data where the cell would be a 1 or a 2 without obscuring that even in some way, usually by changing it from a 1 to a 2 and accounting for that in another cell that keeps the totals the same.  The process can take a long time and is fairly tedious, but it garners good will at the Census.  The general policy for sending this along is that we do it when we can, but if other priorities prevent it we don't send it.

