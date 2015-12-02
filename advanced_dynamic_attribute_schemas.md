# Advanced Dynamic Attribute Schemas

The attribute schema in a dynamic translation can come from a multitude of places… or none!

In general, the schema for a dynamic translation will come either from the source dataset itself, or from a different dataset (such as the database table the data is being written to).

However, there are two other scenarios for providing the output schema: it can come from a text file (or spreadsheet) in which the definition is stored; or it can be actually defined dynamically as a list of attributes in a workspace.

**Table-Based Schemas**

In this scenario, the output schema is stored as some form of table in a text file or spreadsheet; for example:

