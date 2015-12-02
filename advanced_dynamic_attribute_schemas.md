# Advanced Dynamic Attribute Schemas

The attribute schema in a dynamic translation can come from a multitude of places… or none!

In general, the schema for a dynamic translation will come either from the source dataset itself, or from a different dataset (such as the database table the data is being written to).

However, there are two other scenarios for providing the output schema: it can come from a text file (or spreadsheet) in which the definition is stored; or it can be actually defined dynamically as a list of attributes in a workspace.

**Table-Based Schemas**

In this scenario, the output schema is stored as some form of table in a text file or spreadsheet; for example:

Here the author has listed a series of feature types, attributes, and geometry types that define the output schema. In FME they would use this schema by adding a Resource Reader. The format of the Resource Reader would be Schema (From Table):

In the parameters dialog for this Reader, there are parameters that specify which fields in the table represent which parts of the schema:

Geometry type is optional, but used in this example.

Attribute sequence is another optional parameter. It defines a field in the table that records the order that attributes should appear in.

Then, of course, this Reader must be used as the source for the output schema:

The incoming attributes must then be mapped to the outgoing schema. The best way here is the SchemaMapper transformer, since it too can use a lookup table to create its mappings.

<table style="border-spacing: 0px">
<tr>
<td style="vertical-align:middle;background-color:darkorange;border: 2px solid darkorange">
<i class="fa fa-quote-left fa-lg fa-pull-left fa-fw" style="color:white;padding-right: 12px;vertical-align:text-top"></i>
<span style="color:white;font-size:x-large;font-weight: bold;font-family:serif">Sister Intuitive says…</span>
</td>
</tr>

<tr>
<td style="border: 1px solid darkorange">
<span style="font-family:serif; font-style:italic; font-size:larger">
“The great advantage of this method is that you don’t need to edit the
workspace, or edit a dataset, to make schema changes.
Once you change the output schema in the table, then that is automatically applied in the
FME translation. That’s heavenly!”
</span>
</td>
</tr>
</table>

**Constructed Attribute Schemas**

This scenario is a way to construct an attribute schema using lists in FME. The schema is defined by using attributes in the list, for example:

When a feature with such attributes is sent to a dynamic Writer, then this schema is used in preference to any other.

<table style="border-spacing: 0px">
<tr>
<td style="vertical-align:middle;background-color:darkorange;border: 2px solid darkorange">
<i class="fa fa-quote-left fa-lg fa-pull-left fa-fw" style="color:white;padding-right: 12px;vertical-align:text-top"></i>
<span style="color:white;font-size:x-large;font-weight: bold;font-family:serif">Sister Intuitive says…</span>
</td>
</tr>

<tr>
<td style="border: 1px solid darkorange">
<span style="font-family:serif; font-style:italic; font-size:larger">
“The dynamic properties dialog still requires a Reader to be selected,
even if you’re not using its schema for the output. My advice is to add a
Null format Reader and use that anyway. Then you can be sure that
nothing else is being accidentally used!”
</span>
</td>
</tr>
</table>

