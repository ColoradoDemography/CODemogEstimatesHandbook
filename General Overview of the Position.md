---
output:
  word_document: default
  html_document: default
---
# General Overview of the Position

### Position Description and Overview
This description starts with a caveat, it is in no way meant to replace the Position Description Questionnaire, but instead to provide the description from someone in the position.  The call for population estimates is in Statute, meaning that the job is required to be done, however little else is specified in the statute. The tone of this handbook is meant to be informal, but professional with an eye toward mixing the technical documentation with some experience-based and institutional knowledge.  

The Estimates Demographer is broadly tasked with creating population estimates for Colorado Counties, Municipalities, and Conservation Trust Fund Receiving Title 32 Special Districts.  This requires the collection of data on demographic events (e.g. births, deaths, migration), residential housing change, and group quarters populations.  The handbook will detail the specific sources later, but they include the U.S. Census Bureau, Local Governments, and Colorado Department of Public Health and Environment (CDPHE). These data sources are maintained and integrated through a series of files and ultimately an Access database that runs the model.  The accuracy and integrity of these data are the focus here.  This is greatly enhanced by maintaining and encouraging relationships with local government and other government agencies

In addition to the data maintenance and the model, the Estimates Demographer is responsible for running three major data collection efforts, the Residential Construction Survey, the College Group Quarters Survey, and (after the estimates are in draft form) the Conservation Trust Fund Review Process. These three collection efforts are the best opportunity to establish and maintain relationships with the local governments.  These relationships can help to get more accurate data, local expertise, and provide DOLA with a positive face in the eyes of those we are working with.  This helps to further the SDO goals for accurate data and Division/Department goals for outreach and positive impacts.  

Furthermore, the position maintains a relationship with the Census Bureau by sharing our data and expertise while they provide the opportunity to review and comment on their estimates through the Federal State Cooperative for Population Estimates (FSCPE).  This responsibility includes reviewing estimates and data as well as providing data from our surveys.

### Brief Position History

The Estimates position, called many things over the years, has been around since at least 1970.  The position was held by Richard Lin from the inception until 2008.  Richard was a meticulous man that maintained the model using pencil and paper for years until reluctantly using a database for table storage only.  He still calculated the estimates for each place by hand.  The notebooks and most of the paper files that come with the position were created by him.


Eddie Hunsinger (Currently the State Demographer of Alaska and active in FSCPE) was the next person to hold the job, from about 2008 through the 2010.  Eddie is responsible for modernizing the position and creating the original Estimates database.  He also was interested in alternative estimates for Age and using Regression which are in the "Other" directory of the Estimates folder. Eddie created many of the Intercensal (fixing any error in our estimates made based on the Census 2000 base) materials as well as the skeleton of the Residential Construction Survey

Deying Zhou took over the position from Eddie in 2010.  She was able to extend Eddie's database work, including creating the first set of Basic Geographic Unit (BGU) estimates that would be generated within the database. These estiamtes are for each piece of the State identified by the county, municipality, and special district (including overlaps with other districts) that each geography has.  Breaking the state into unique geographic areas that we estimate for. This paved the way for a much faster and easier process generating estimates for the special districts.  In her last year, Deying directed IT in the creation of the EFiling Portal for collecting the Residential Construction Survey data online and processing it via a database.

I (Rob Kemp) took over in November of 2013.  I've improved the integrity of the input data dramatically, introducing vintaging to almost all input data for all of the models.  Another important step was implementing a full housing unit method for the BGU model rather than a proportional sharing model.  I ahve also extended some of the data processing and sped up many internal data requests via R.  

### General Estimate Concepts

I've already used a few of these terms at the outset, but I wanted to make sure that the general concepts are clear before the details get covered.  The main focus of this section will be vintaging with a few definition terms for the methods.  The county model uses a component method that relies on take the base population (Census 2010 for this decade, moved from April 1, 2010, to July 1, 2010) and track change by adding natural increase (births minus deaths), group quarters change (any place with shared facilities, see Census documentation for more detail, tracked at the facility level), and net migration (taken from the Census' IRS based method).  The city and county model uses a "controlled" (meaning it sums to the county-level) housing unit method that allocates people based on housing unit change using vacancy rates and persons per household from the Census-base and tracking group quarters population to get a total.  The BGU model uses the housing unit method as well, but proportionally shares out group quarters change.  These are considered to be "postcensal" estimates because they are after the last Census, but before the next.  Intercensal estimates are postcensal estimates that are adjusted after they reach the next Census for any error they may have accumulated across the decade. Each Estimate is made for an estimate year spanning July 1 to June 30, which is also the State's fiscal year.

Vintaging is a process where the entire time series of postcensal estimates are updated each year the estimates process is run. This allows for updated data or methods for any year in the time series to be taken into account.  This is important because each estimate for one year impacts the next because populations build on themselves.  This also allows for local governments to correct errors in previous years that make all following years more accurate.  Unfortunately this means that every year there is a new estimate for that first year in the series.  We notate this by using the latest year in the series and naming the vintage after it.  For example, if the time series for the estimates spans from 2010 to 2014, then the vintage would be called 'Vintage 2014'.  Almost all of the input data is "vintaged" meaning that it is recreated and updated for each set of estimates and stored separately.



### CTF Estimates Review Shiny Apps:



https://gis.dola.colorado.gov/apps/ctf_estimates_final/

https://gis.dola.colorado.gov/apps/ctf_challenge_data/

https://gis.dola.colorado.gov/apps/rcs_data/