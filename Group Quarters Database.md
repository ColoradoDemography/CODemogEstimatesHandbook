---
output:
  word_document: default
  html_document: default
---
# Group Quarters Database

# Outline
3. Group Quarters Database
	1. Purpose
	2. Organization
	3. Updating
	4. Queries
		1. Aggregations
		2. GQR Update
			1. Set-up new GQR based on last years using queries.

## Purpose
The Group Quarters database originates with me (Rob).  It replaces a very unweildy spreadsheet that we'd previously used to track these places.  The key difference is that I've created a difference between aggregations (e.g. all of Colorado State Universities dorms reported together) and facilities (e.g. single dorms or prisons).  The database also helps simplify the reporting process for the Census Bureau's Group Quarters Request (GQR).

## Organization 
This section will go over specifics on which tables are included and what functions they serve. 

### Adding a facility
We seem to get a new facility or two every year, but there wasn't really a great process for adding them.  I continued that trend and ahve been using the following process that seems to work, but is very brute force.

	1. Sort the Facility List table on the ID or Numeric ID table. 
	2. Start by getting the Cou (numeric) and COUNTY (2 character String) as well as the PLACE columns updated.  Entityname is the city or county (if unincorporated) CountyName is exactly that.  Parentinstitutionname is for use mostly at colleges, but could be other multi facility areas. Type it if you can using the ACS type codes you can find online or in the filing cabinet. Fill out as much of the remaining data as possible and don't forget the population number. Also make sure to point out which year we added it  in the YearAdded Column.
	3. Create the ID number by adding 1 to the last ID number in the row (assuming you've sorted it by ID). Retype in the Numeric ID column.
	4. Create the UID by truncating (combining) the COUNTY, PLACE, and ID variables together.
	5. Enjoy the victory.
## Updating the Database
One of the trickiest parts of the estimates process involves updating and mainatining the group quarters data.  This process is designed to give the clearest picture I can to a very detailed process.

I generally approach it like this:

	1. Prisons
	2. Areas from the RCS/GQ submission
	3. College GQ Survey
	4. Selecting facilities for inclusion and creating master
	5. Updating GQ Master for inclusion in process

### Prisons

There are two types of prisons that we can easily collect data on: state facilities and federal facilities.  Both of these entities has data online for us to go download.  They all live in the FacilityList_Master table with a Type code of 103 for State and 102 for federal.  I filter on the type I'm updating for Prisons only.  The other types of facilities aren't super reliably typed.

To updated the State prisons we can look at the Department of Corrections website and find the Monthly Population and Capacity Reports here: https://www.colorado.gov/pacific/cdoc/departmental-reports-and-statistics.  We use the June report for the estimate year, so in 2015 we'd use the June 2015 report.  The report lists each prison and we use the "Facility Population" column to get their total population to input into the table.

To update the federal prisons, we can look at the Bureau of Prisons site and get those numbers by selection Colorado as the "State" here: https://www.bop.gov/about/statistics/population_statistics.jsp .  We don't get detailed timing information, but I try to log on close to the end of June of my estimates year.  Basically, I take whatever they have at the time I look, but it should be close to that time.

### Local Area Submissions
We don't get a lot of submissions, but some areas actually send us information on local group quarters counts.  Typically it is larger areas like Aurora or Grand Junction, but sometimes places like Clear Creek send us good data as well.  I tend to enter this around April to make sure we have time to get it in and checked.  Most of the places use our spreadsheets, but not all.  I put responses into the GroupQuartersData>GQSurvey>XXXGQSurvery>GroupQuarters_RCS2015 folder then move them to another subfolder called "Processed" once I've entered them.  These facilities are all in the FacilityList_Master table and if they aren't you can add them using the process outlined above in the Organization section.

### College Group Quarter Survey
It's not often remembered, but we do survey all of the colleges in the state to ask for information on their group quarters.  The material for this survey are in the J>Estimates>GroupQuartersData>GQSurvey>XXXXGQSurvey>College and Univ Survey. I basically send a spreadsheet with the data we have for the college along with an email explaining the process to each contact individually. It's not a terribly complicated survey, but I will outline my procedure.

	1. Copy the files from the last year to the current year to make sure you don't overwrite anything. I hide them in an "Old Files" folder I later delete.
	2. Verify contact updates from emails and last year's forms are in the Aggregation table in the GroupQuartersDatabase.
	3. Update Last years spreadsheets with submitted data and contacts from areas we heard from.
	4. Update the email template to reflect the new dates and pick a new due date.  I've used 3 weeks and 4 weeks from when I send it out.  Doesn't seem to matter.
	5. Update emails in the email list to what  is correct in the Aggregation table.
	6. Create a mail merge to generate the proper text for each email.
	7. Send and individual email with the proper text from the template and excel sheet in each one.  I try to keep tract of this in the contact list if I can.
	8. Place submissions in a Responses folder and once you've put them into the database, move them to a subfolder called Processed.

Now for some notes.  We get different data from different places.  The spreadsheets have what we get from each place.  Sometimes we get dorm/facility level data, often we just get total counts.  Total counts get entered in the Aggregation table while facility data is in the Facility List_Master table.  These positions turn over a TON.  I'd go check out the Residence Life website for each school if an email bounces or gets returned.  Usually you can find someone fairly high ranking to send it to.  That usually works.  I've been able to get to zero bounces every year using that method.

### Creating the GQ Master
I don't store the Aggregations and the FacilityList_Master together because they aren't the same and it was causing issues.  The problem there is that the Estimates database needs that information in one table, so I created the EstimatesGQMaster2010 table to deal with this.  It get recreated every year without bothering the other two more final tables.  There is a macro with the specific queries, but I'll go through the process here as well.

	1. We need to get the Aggregation table updated, so I use a query to sum up all of the facilities in the FacilityList_Master to generate the Aggregation.
	2. The EstimatesGQMaster 2010 table is re-generated each year, so I make a new one to start with.
	3. Then, I append all of the aggregations that are not in the Facility_List to the EstimatesGQMaster2010 table.
	4. There is a flag on the EstimatesGQMaster2010 table for inclusion in the Estimates process called EstimatesUpdate. Queries 3, 4, and 5 update that field to a 1 for Prisons, Colleges, and Juvenile Residential Treatment Centers.
	5. Next, I go through each line and check for inclusion in the process using the below criteria.  If the facility meets the criteria, I flag it with a 1 and make any needed changes to the data.
		a. Complete time-series - If not and we need to include, carry forward the previous values since that will result in asusming no change.
		b. Previous inclusion and timeseries variation.  Sometimes we only get data once, but it will have changed estimates due to facility size 		    variation.  Make sure to include these.
		c. Mesa, Grand Junction, Aurora, and Clear Creek generally give updates each year, include those always.
		d. Check Aggregations for anything that looks like doubling. Colorado Mesa University had that for one year that I found and fixed.
	6. Ensure that the Estimates database is still linked to the new table
