---
output:
  word_document: default
  html_document: default
---
# BGU and CTF Estimate Process

## Process Notes

The BGU process is the process we use to build special district estimates.  BGU stands for Basic Geographic Unit.  That means that each BGU is a geographic area uniquely identified by the County, Place, and Special Districts that are overlapping the area.  We've recently moved this level of the process to the housing unit method as well.  We then use these to build the Special District estimates used by the CTF program.  

## Database Specifics

### Tables

#### BGU Process

BGU_Estimates_2010:  Master table for the BGU process

BGU_Estimates_2010_Overwrites: This table holds any forced numbers, including housing unit totals from the RCS process, for inclusion in the process.

Query1: County-Place sums for use in the BGU process.

BGU_Estimates_2010_with_overlap: Overlap BGU table for completion of the CTF process to build district totals. This table has all the BGUs needed (duplicated for overlaps) to build District totals.

BGU_Estimates_2010_overlap: Transition table for overlapped BGUs Table

#### CTF Process

20XXCTFEstiamtefinal2: This table shows all district totals and the pieces that create the BGU.

### Queries

#### BGU Process

BGUEstimates2010_Step00: Updates the Unique ID for any new BGUs in the BGU table.

BGUEstimates2010_Step00a: Updates the Unique ID for any new BGUs on the Overwrites.

BGUEstimates20XX_Step01:  Nulls out the BGU master table and then primes the Table with either the Census value or previous year's value for persons per household and the vacancy rate.

BGUEstimates20XX_Step02: Proportionally allocates housing units and group quarters to the requisite BGUs based on the county-place that they reside in.

BGUEstimates20XX_Step03: Module that incorporates the overwrites for incorporated places.

BGUEstimates20XX_Step04: Creates unincorporated area table.

BGUEstimates20XX_Step05: Proportionally allocates housing units and group quarters to unincorporated areas.

BGUEstimates20XX_Step06: Runs overwrites for unincorporated areas.

BGUEstimates20XX_Step07: Creates total housing unit sums by place.

BGUEstimates20XX_Step08: Creates a table of differences between the control totals and the sum of the BGUs.

BGUEstimates20XX_Step09:  Creates a table of the place sums of the BGU totals including only BGUs that are allowed to grow.

BGUEstimates20XX_Step10: Proportionally allocate differences (usually attributable to growth in the housing units at the place level) to BGUs that are flagged for growth.

BGUEstimates20XX_Step11: Create a new set of place-county sums of BGU housing units

BGUEstimates20XX_Step12: Updates areas where additional units are allowed (usually unincorporated areas) to capture any differences do to rounding in the proportional attribution process. 

BGUEstimates20XX_Step13: Creates a household population total using the new housing units.

BGUEstimates20XX_Step14: Creates a household population sum by county and place from BGUs.

BGUEstimates20XX_Step15: Creates a difference table between the county-place population control totals and the BGU sums.

BGUEstimates20XX_Step16:  Adjusts the BGU based on the county-place it is in to ensure it sums to the control totals.

BGUEstimates20XX_Step17: Creates another table of BGU household population totals by county-place. 

BGUEstimates20XX_Step18: Updates the areas that are allowed to be adjusted to take the rounding issues from the proportional sharing. 

BGUEstimates20XX_Step19: Re-calculates the persons per household, vacancy rate, and vacant housing unit counts to reflect the new population and housing unit counts.

BGUEstimates20XX_Step20: Creates a total population from the group quarters and household population columns.



BGUEstimatesOverlapped_step01: Creates the with overlap table showing BGUs with overlap.

BGUEstimatesOverlapped_step02: Creates the transition BGU overlap table.

BGUEstimatesOverlapped_step03: Updates the overlap table with Unique IDs.

BGUEstimatesOverlapped_step04: Appends overlaps to with overlap table.



#### CTF Process