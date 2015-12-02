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