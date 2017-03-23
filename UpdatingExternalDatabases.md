# Updating External Databases
### Connecting to PostgreSQL Databases
### Updating PostgreSQL Databases for Estimates

1. Create copy of old table in case of failure (also for posterity at the moment).  Use a call like this as a 'Pass Through' query in Access: CREATE TABLE estimates.muni_pop_housing_old AS SELECT * FROM estimates.muni_pop_housing.  You'll need to change the name of the tables as needed and you may need to change the back up table name.
