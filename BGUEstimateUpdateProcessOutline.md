---
output:
  word_document: default
  html_document: default
---
# BGU Estimate Updates Process
1. Update the 'BGU_Estimates_2010' table with the latest year (i.e. add all columns for the year 2016 for v2016).
2. Update the tables 'CTFDistrict_NewBGUAppends' and 'CTFDistrict_ExistingBGUUpdates' with new data from Todd or GIS Person on new districts or any other updates from boundary data. Note of Vacancy: Do best to maintain Vr from original (larger) BGU when allocating vacant v occupied.
3. Update the queries for New Districts and Updates if needed at all.
4. Run the set of BGUEstimates New Data Queries after you are 100% sure the tables and queries are right. These are append queries.  You can't re-run these without manually updating the tables first.  Otherwise you'll be doubling some areas.
5. Create a new set of queries for steps 1 to 20 for  the new vintage year and update them all appropriately to line up and create new year estimates (i.e. make new queries with 2016 for v2016 and move 2014 to 2015, 2015 to 2016, etc.).