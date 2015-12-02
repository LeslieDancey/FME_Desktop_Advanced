# Schema Handling in Dynamic Translations

Dynamic Translations still use a schema, but it is not necessarily a carbon copy of the source dataset.

**Dynamic Translation Settings**

Opening the feature type properties dialog for a dynamic translation reveals the checkboxes that turns on this behavior.

For a Reader, all that is really happening is the merge feature type setting is turned on:

For a Writer, there is a special Dynamic option (it’s not just a feature type fanout):

So, it is possible to create a dynamic translation by turning one or both of these settings on manually; there’s no necessity to do so at the time the workspace is created.

The two extra parameters on the Writer are to control the source of the schema being used on the output dataset.

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
“Yes, a dynamic translation is often used to handle a variety of source
datasets, by automatically duplicating the incoming schema – feature
types, attributes, geometry types – on the output.
However, it’s also possible to dynamically select the outgoing schema from a completely
different location, or from an attribute in the data, or even by constructing a virtual
schema in the workspace!”
</span>
</td>
</tr>
</table>

**Schema Sources**

The schema sources parameter allows the user to choose where the destination schema is going to be obtained from.

By default, this parameter is set to whatever source dataset is being read. That way the output schema is always a duplicate of the input.

However, it can be set to use any Reader dataset – in any format – as the source for the outgoing schema. In the case where a Reader is only required to provide a schema, and not data, then it would be added as a Resource Reader.

For example, here the author has opened that parameter and is changing the output schema from the default (input dataset) to a standard corporate schema that is defined in PostGIS and has been added as a Resource Reader:

This is useful when you want to enforce a particular output schema, but it means that you have to ensure that the data being processed will match the feature types available in that schema.

If you write data to a dynamic Writer, and the feature types of that data do not match what is provided by the schema then it will be dropped:

Consider this behavior a sort of “Unexpected Output Remover”.

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
“In this scenario the “Dynamic” part of the translation is the destination
schema being fetched at run time.
For example, if the corporate schema (above) were to change, the workspace feature
types would not need updating. They would be automatically ‘updated’ when the
workspace is run.”
</span>
</td>
</tr>
</table>

**Schema Definition**

The Schema Definition parameter opens a dialog with a number of options:

These options are where a user can become very creative with their dynamic workspaces.

Remember, a schema is composed of three basic parts: Feature Types, Attributes, and Geometry Types. These settings give the author control over each part of that schema.

By default, each part is obtained from the incoming schema, whether that’s a real Reader or a Resource Reader. But these settings let the author pick alternative sources.

For example, the author could decide that the feature type name will be fixed (i.e. all output must match this set value), that the attribute definitions should come from feature types defined by an attribute value, and that geometry is set to a fixed type.

Here each incoming feature is assumed to possess an attribute called OutputLayer.

That attribute defines what feature type (layer) the data will be written to.

It also defines the Reader (or resource) feature type that the attribute schema will be taken from.

Finally, it specifies that the geometry of the output features must be area (polygon) features. Non-area features will be dropped.

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
Adding or Deleting Attributes
Even in a dynamic translation, sometimes you need to add or delete attributes from the output
schema. This is very simple to do.
</span>
</td>
</tr>
</table>

