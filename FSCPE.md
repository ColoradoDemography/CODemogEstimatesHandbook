# Federal State Cooperative for Population Estimates

# Outline
1. County Estimate Review
	1. Hints and Tips - We aren't ready usually
2. Housing Unit Review
	1. Timing and RCS
	2. Methodology
3. Subcounty Population Review
4. Group Quarters Report(GQR)
	1. General Thoughts and Process
	2. Query Structure (Refer to GQ DB?)
5. Vital Statistics Request
 	1. Totals and Verification
 	2. Race and Supression Sheet
6. Meetings
	1. Fall
	2. Spring



# Vital Statistics Request

In the late summer, about a month after the Group Quarters data are submitted, the Census bureau will send out the County Vital Statistics Report for their next vintage.  They ask for two products, the county level births (which are 'required') and the race detail for births (which are optional, but we provide in a typical year).

## Totals and Verification

The total birth and death counts for each year are sent along by Kirk Bol or someone in his unit from CDPHE at the beginning of July.  We can get provisionals before this, but that is when the final births and deaths are ready.  

Total counts for the counties are on a fiscal year basis, so for the year 2012, the counts included births from July 2011 to June 2012.  In general Kirk sends a file with monthly data and calendar year totals that need to be re-aggregated into the fiscal year and then moved the the birth and death master excel files.  This is generally done by the end of the previous Estimates cycle since ours are due in August.  Therefore we can generally just take that data from there and place it into the templates.  This makes things a bit easier for us, we just need to verify the geographic fields and such.

After I put them all in the spreadsheet template provided, I run a few checks on them including summing to the State totals and checking them individually against my Masters.

## Race data

We have generally provided the Census with our race detail from the CDPHE data Kirk sends.  It comes in microdata and I used R to process it and turn it into a usable format, but it could be done in Access or other databases.  After I have done that I put it into a spreadsheets (examples of which live here: J:\Estimates\VitalRecordsData\FSCPESubmissions\2014VintageVitalStatsSubmissions\2013BirthsAdjust).  The spreadsheet helps keep the totals for the State apparent as we change numbers to meet our Supression agreement with the CDPHE.  Per our agreement we are not allowed to send out data where the cell would be a 1 or a 2 without obscuring that even in some way, usually by changing it from a 1 to a 2 and accounting for that in another cell that keeps the totals the same.  The process can take a long time and is fairly tedious, but it garners good will at the Census.  The general policy for sending this along is that we do it when we can, but if other priorities prevent it we don't send it.
