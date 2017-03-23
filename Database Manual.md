# Database Manual

# Outline

1. Database Manual
	1. Organization
	2. Table Definitions
	3. Reports and Selectors
	4. Macros
	5. Archiving



## Archiving the Database

Toward the end of March through April it is time to think about archiving the old Database. This process has varied over time, but I have a procedure that seems to work well for me.  We used to archive the DB and ALL of the files associated, basically the whole directory.  That was a bit bloaty and sort of overkill. I've outlined my process below, it's pretty simple.

#### Archival Process
	1. Create a copy of the database on our local machine.  I rename it with the vitange name on the end, so for vintage 2014 it's "Estimates 2010-20v2014.accdb".
	2. Convert all of the linked tables (including those from Oracle) to local tables.  This makes the database self-contained and unable to be changed based on new data in the input files for the vintage. I highlight all of the linked tables in each section > right-click > then select "Convert to Local Table."
	3. Save the local database copy.
	4.  I like to keep the previous vintage in the main Estimates directory as well as archived.  So delete the previous vintage database already in the Estimates directory and then replace it with a copy of the one you just made.  BEFORE you do that, double check that the one you're going to delete is archived.
	5. Right-click on the local copy you've been using and compress the database into a zip file.  If you want to add other files to that, you can.  I did in 2013, but I'm not sure what purpose I thought that would serve. Rename the zipped file "VintageXXXX" based on what vintage you're archiving.
	6. Place the new zip file into the Archive sub-directory of Estimates. 
	7. You can delete the local copy.
	8. Send out an email to the staff to let them know what you've done and where to find the data. They'll appreciate it.
	9. Continue building new vintage in the DRAFT folder until you're ready then move it to the main directory.
