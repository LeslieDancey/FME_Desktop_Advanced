# Conditional Attribute Values

Conditional Attribute Values are a tool that can be used to replace many existing transformers of the same type.

**Transformer-Based Attribute Mapping**

The Basic FME Desktop training course includes a section on Conditional Filtering, and explains how to apply conditions to data in order to split or divide it into multiple streams.

In this example, the AttributeFilter is being used to divide data on the basis of a postal code attribute value:

Similarly, a Tester or TestFilter transformer can be used to divide data in various ways.

So filtering transformers divide data up into separate streams in the workspace. The question is: what happens when the scenario requires a new attribute to be created based upon the original attribute value?

Technically, the following works, but it is far from elegant:

There are just far too many AttributeCreator transformers. Imagine if there were 100 values to handle! The workspace would be enormous!

In that scenario, the solution would be to use a simple AttributeValueMapper transformer:

However… what if the original attribute required a more complex condition to carry out the mapping? In that scenario something even more advanced would be required: Conditional Attribute Values.

**What are Conditional Attribute Values?**

Conditional attribute values are when the author sets an attribute value, but conditional upon a number of tests that must be first applied to the data.

The option for conditional attributes is found in the drop-down dialog on most transformer parameters. In the AttributeCreator, it appears like so:

The Conditional Definition dialog looks like this:

Like the AttributeValueMapper, a series of conditions map to different values. However, in contrast to the AttributeValueMapper, this dialog allows much more complex conditions than a simple 1:1 mapping. That’s because full test capabilities are built into this dialog.

The test capabilities are accessed by double-clicking in the Test Condition field. That opens up a dialog almost identical to that used by the Tester and TestFilter. A number of complex conditions can be defined in order for this test to be passed.

The output value for a passing feature can be set here at the foot of the dialog, or back in the Conditional Definition dialog:

<table style="border-spacing: 0px">
<tr>
<td style="vertical-align:middle;background-color:darkorange;border: 2px solid darkorange">
<i class="fa fa-bolt fa-lg fa-pull-left fa-fw" style="color:white;padding-right: 12px;vertical-align:text-top"></i>
<span style="color:white;font-size:x-large;font-weight: bold;font-family:serif">NEW</span>
</td>
</tr>

<tr>
<td style="border: 1px solid darkorange">
<span style="font-family:serif; font-style:italic; font-size:larger">
The Output Value
field does not
necessarily need
to be a value. It
can be any action
on the usual dropdown
menu,
including Null or
Stop Translation.
</span>
</td>
</tr>
</table>

When the conditions are set then the original dialog – in this case an AttributeCreator – looks like this, with the number of conditions defining the number of possible values:

**When to use Conditional Attribute Values?**

Conditional attribute values are great for when you need to map (or set) an attribute in relation to the value of an existing attribute, when the conditions are more complex than can be handled in a simple AttributeValueMapper or RangeValueMapper transformer.

<table style="border-spacing: 0px">
<tr>
<td style="vertical-align:middle;background-color:darkorange;border: 2px solid darkorange">
<i class="fa fa-quote-left fa-lg fa-pull-left fa-fw" style="color:white;padding-right: 12px;vertical-align:text-top"></i>
<span style="color:white;font-size:x-large;font-weight: bold;font-family:serif">Professor Lynn Guistic says…</span>
</td>
</tr>

<tr>
<td style="border: 1px solid darkorange">
<span style="font-family:serif; font-style:italic; font-size:larger">
"If you’re using the ?: operator in an arithmetic editor, then well done you!
But that’s now a scenario where you could instead use the conditional
values technique."
</span>
</td>
</tr>
</table>

A colleague is working on a workspace to calculate the flood risk due to tsunami for all addresses in the city. The risk is adjudged to be a combination of closeness to the shoreline and elevation above sea level, and is calculated using this table:



Your colleague has created the workspace up until the point at which the calculations need to start, and has asked for your assistance in finishing the project.

**1) **Start Workbench

Open the workspace 

C:\FMEData2015\Workspaces\DesktopAdvanced\Exercise5b-Begin.fmw.

To find out what data we are dealing with, add Inspector transformers throughout the workspace and then run it - or else use Run > Run with Full Inspection from the menubar.

You’ll probably want to inspect the source features types (or the Reprojector, since the CDED data is a different coordinate system). You’ll also want to inspect the AttributeRenamer output.
Don’t forget you can set a Group-By in an Inspector's parameters, which may be of use in visualizing which addresses are in which zone.