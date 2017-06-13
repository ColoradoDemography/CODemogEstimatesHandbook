---
output:
  word_document: default
  html_document: default
---
# Remaining Work for CTF and City and County Estimates

1. Add in the responses from the RCS (J:\Estimates\ConstructionData\LocalUpdateData\v2016ResidentialConstructionSurvey) for each district to the BGU_Estimates_2010_Overwrites table and move response to Processed.
2. Re-run all BGU, BGU Overlapped, and CTF Queries
3. Finalize all challenges.
   1. Kremmling is done.
   2. Dacono will require new master creation, but waiting on clarification.
   3. Washington needs BP added in too.
   4. Delta will require new master creation.
   5. Parker just made a notice, will require some help.  Seems like an error is in the housing data.
   6. NOTE: You can just alter the Master for each data type and the Annual Construction table if you'd rather not run the R code to generate the new masters.
4. Send Out notification to counties where other places changed by more than 50 or so.  Use your judgment, could be less if it might matter.
5. Summarize the outcome of all challenges in a table for records.
6. Prepare to run the CTF Special District Challenge
   1. Turn Report Table4_Draft_2016 into a PDF (should show the district estimates for Vintage 2016).
   2. Place PDF into the State Demography Office website folder on Google Drive.
   3. Get a Share URL by right clicking on the document.  Make sure sharing is set to Anyone on the Internet.
   4. Go to Estimates database and export the query "LGISSurveyContactInfoSD" to a csv
   5. Import the new CSV to MailChimp for the CTF_SpecialDistrict list.
   6. Create new campaign for that updated list with a link to the PDF as the review data.
   7. Process responses (typically using the Overwrites table)
   8. Finalize Challenges
7. Finalize Estimates
   1. Get final births and deaths from Kirk.
   2. Re-run all queries with final data and overwrites.
   3. Once you're sure, send the "DirectDistributionPull" query as an Excel file to Cynthia Thayer by August 1.
   4. See Tables>Vintage 2015 for list of tables to make.
      1. Use corresponding queries
   5. See DatabaseUploads for tables to make to upload to the database. Check with Cindy.