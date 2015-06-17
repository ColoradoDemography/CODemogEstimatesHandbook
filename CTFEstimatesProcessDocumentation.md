# CTF Challenge Process
The Conservation Trust Fund estimates are required to be provided for a review period by the local governments they are made for.  This process is typically carried out in the month of June, giving enough time to process and finalize estimates by August 1.  The process includes making draft tables and notifying the local governments of their ability to review them on the web.  The process must last 30 days and must go through Tamra Norton (or the current CTF administrator).

#Preparations
The first part of the process comes after you have completed and reviewed the first draft of estimates for at least the Counties and the Cities (they have an August 1 deadline so they take priority.  

There are two main jobs to the preparations: setting up the website with new text, deadlines, etc and sending out the email to an updated mailing list notifying the areas of the process.

It would also be a good idea to check with challenges from the previous year to see if overwrites need to be carried forward.  For example, in v2013 Grand Junction successfully challenged their Vacancy rate, but then when reviewing v2014, they saw that the 2014 Vr was back high again, but shouldn't have been had the overwrite carried forward.

# Challenges
After the email has been sent, periodically people will respond. We typically to not log contact changes or similar items as full challenges.
###Logging Challenges
Often the place will contact you directly to start the process, asking a question about the estimates that will turn into a challenge.  Once you've decided that you might change something, make sure that they entity notifies Tamra and that she has logged the challenge and sent you the Challenge information (Place Codes and a "DLG" code that represents the official challenge number).  After she logs the challenge the subsequent emails about the data and changes can leave Tamra out until the final determination is made.

###Contact Changes

Done in the Estimates database in the table "CityandCounty_Contacts" or "District_Contacts".  Also make sure to put a Word document with the email into the folder for the most recent challenge period (example here for Vintage 2013: J:\Estimates\Adjustments\LocalReviewsAndChallenges\v2013ReviewsandChallenges).

The emails that are used to send out the review are not these emails, but instead are the listed CTF Administrator for each area.  These are updated each year during the certification process for CTF and are generally more accurate.  The lists are currently run using the Mailman system, although there was some work done towards using Google Groups if they can add bulk uploading and management options.  The url for each group is below, an important note is to watch the notification settings before making any changes to the lists or people get emails and worry that they've been removed unnecessarily.

County: 
email - ctf_county@mailman.state.co.us
url - http://mailman.state.co.us/mailman/admin/ctf_county

Municipality:
email - ctf_muni@mailman.state.co.us
url - http://mailman.state.co.us/mailman/admin/ctf_muni

District:
email - ctf_district@mailman.state.co.us
url - http://mailman.state.co.us/mailman/admin/ctf_district

List Password: demography

### Data Challenges
When an entity replies, they often will immediately supply some justification or supporting data, but not always.  There are two situations where they may not: a calculation/model error or they just didn't know they should.  It is important to get some documentation of the claims.  Most often it is a housing unit count issue and the best thing to get is a set of permits or COs.  Otherwise, we can be fairly creative including looking at water billing (for totals and vacancy), parcel data if we know the timing, or other data that makes sense.  The important thing is to try to get the data the most accurate you can while making sure the place understands why the estimate is what it is.  You don't always need to "give in" and take whatever the place gives, but you need to educate them on the process and requirements so that you can build a relationship.  Throughout the process remember that "challenges" aren't bad, they are a great thing because they help make our estimates more accurate and establish a relationship with the place.

*****Add a more formal section on data vs challenges*******
### Replies

Once you've decided on a path of action and preliminary run it by the place (hopefully with their approval) there are two more steps to completing the process for them.  The first is to look at what that change will do to any impacted areas that didn't challenge.  For example, changing the housing units in one place will alter the population (potentially) for every other place in the county.  You'll want to do this before you officially accept the challenge to check of other oddities you may need to work out.  Another important point is keeping Elizabeth (the State Demographer) in the loop on both the challenge and impacted areas.  After you've gotten the challenge finalized, send a reply to the place that challenged letting them know the results and providing any needed explanation (it is a good idea to note that you'll be letting other places in the impacted area know).  Make sure that Tamra is included on the email and print it out for the records.  Keeping the changes made and entities impacted in one big spreadsheet is a good idea (see example: J:\Estimates\Adjustments\LocalReviewsAndChallenges\v2013ReviewsandChallenges\DetailedChangeSummary.xlsx).

### Record Keeping

It is important to figure out a good system for tracking all of this on your own, but there are a few things that NEED to happen.  The first is creating a spreadsheet (see example here: J:\Estimates\Adjustments\LocalReviewsAndChallenges\v2013ReviewsandChallenges\Summary of Challenges 2013.xlsx) that track challenges and base data to look at as well as changes and notes.  This will help if we ever need to go back.  You also need to print out the challenge letter, the documentation letter from Tamra, and preferably the response letter.  These documents should all be kept in a directory names vXXXReviewsandChallenges in the  J:\Estimates\Adjustments\LocalReviewsAndChallenges directory where the XXXX stands for the vintage being reviewed.  