# Database Optimization

Using database functionality inefficiently will do more to degrade performance than almost anything else in FME.

Besides the previous performance tips and tricks, there are some that apply only to databases and some that apply only to specific formats of database.

Database Reading

Reading and filtering data (querying) from a database is nearly always faster when you can use the native functionality of the database.

For Readers this means using the various parameters that occur in the Navigator window of Workbench, like this SQL Server Reader:

Here there is a WHERE clause and a bounding box. When you set these then FME’s query to the database includes these parameters.

This is way faster than reading the entirety of a database and filtering it by attribute (Tester) or geometry (SpatialFilter).

Additionally, Reader feature types often contain a set of parameters containing WHERE clauses and SELECT statements, which mean you can set a query to apply to just one particular table in your workspace: