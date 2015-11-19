# Database Optimization

Using database functionality inefficiently will do more to degrade performance than almost anything else in FME.

Besides the previous performance tips and tricks, there are some that apply only to databases and some that apply only to specific formats of database.

Database Reading

Reading and filtering data (querying) from a database is nearly always faster when you can use the native functionality of the database.

For Readers this means using the various parameters that occur in the Navigator window of Workbench, like this SQL Server Reader:

Here there is a WHERE clause and a bounding box. When you set these then FME’s query to the database includes these parameters.

This is way faster than reading the entirety of a database and filtering it by attribute (Tester) or geometry (SpatialFilter).

Additionally, Reader feature types often contain a set of parameters containing WHERE clauses and SELECT statements, which mean you can set a query to apply to just one particular table in your workspace:

Besides Readers, transformers can also be used to query database data. The best to use is the SQLExecutor (or SQLCreator) as these pass their queries to the database using native SQL. If you don’t want to write SQL then you can use the FeatureReader transformer; but be aware this transformer is more generic and won’t give quite the same performance.

The SQLExecutor is particularly worth being aware of, as it issues a query for each incoming feature. This can be useful where you need to make multiple queries.

For example, here a query is issued to the database for every address feature that enters the SQLExecutor.

Generally the output from the SQLExecutor is an entirely new feature. If you want to simply retrieve attributes to attach to the incoming feature, then the Joiner transformer is more appropriate:

<table style="border-spacing: 0px">
<tr>
<td style="vertical-align:middle;background-color:darkorange;border: 2px solid darkorange">
<i class="fa fa-quote-left fa-lg fa-pull-left fa-fw" style="color:white;padding-right: 12px;vertical-align:text-top"></i>
<span style="color:white;font-size:x-large;font-weight: bold;font-family:serif">Jake Speedie says…</span>
</td>
</tr>

<tr>
<td style="border: 1px solid darkorange">
<span style="font-family:serif; font-style:italic; font-size:larger">
“FME is fast, but if you can filter or process data in its native
environment, it’s likely to be faster still.
For example, a materialized view (a database object containing the results of a query) is
going to perform better than reading the data and filtering it in FME. Similarly, a SQL
Join is going to perform better than reading two tables into FME and using the
FeatureMerger transformer.
Sometimes it really is a case of working smart, not hard!”
</span>
</td>
</tr>
</table>