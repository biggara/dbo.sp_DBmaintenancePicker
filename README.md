# dbo.sp_DBmaintenancePicker
Create this to create maintenance cycles. It grabs a list of databases, sorts by size and then using mod returns the remainder of its row value divided by the chosen cycle. Current cycles are monthly (uses end of month getdate) and weekly (7), plan to add other named and allow you to just input an int. 

Current parameters (@cycle and @overridedate) can be left blank and it will run a a monthly loop and the current date.

The ultimate goal for this was to return a comma seperated list of databases to pass to Ola Hallengrens IndexOptimize script. 
Its 90% of the way there I am actually just having trouble understanding how to do somethign like this:

declare @tobemaintained varchar(max) 
exec _dbautility.dbo.sp_DBmaintenancePicker @cycle = 'monthly', @overridedate='10/30/22'
print @tobemaintained


EXECUTE _dbautility.dbo.IndexOptimize
@Databases = @tobemaintained,
@FragmentationLow = NULL,
@FragmentationMedium = 'INDEX_REORGANIZE,INDEX_REBUILD_ONLINE',
@FragmentationHigh = 'INDEX_REBUILD_ONLINE',
@FragmentationLevel1 = 50,
@FragmentationLevel2 = 80

Any help or tips appreciated, if you can use it thats great also!
