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

You’ll see how the addresses are assigned a zone denoting their distance from the shoreline, and also possess an elevation.

**2)** Assess Methodology

Before we get onto a full set of instructions for the exercise, try to consider how you might go about this task.

You’ll need to consider:

- Can the data be mapped directly, or does it need filtering first?

The zone is fairly easy to handle, because it is a fixed value (100, 200, and 300).
However, elevation is trickier because they are not fixed values; elevation could be any single value from 0 to 60. So mapping elevation values would need 60 x 5 = 300 combinations!

- Which transformers would you use?

If you want to filter the data then the Tester and TestFilter transformers seem to be the most obvious candidates, with maybe the AttributeRangeFilter. To map data, either the AttributeValueMapper or AttributeRangeMapper appear to be the best. But as a whole, we’re looking to set attribute values, so why not just use the AttributeCreator?

- Should you combine methods?

Perhaps a combination method would work best, where you filter the data partially and then map it? If so, which data do you filter by and using which transformers?

- Which will produce the most aesthetic workspace?

Best Practice should always play a part in any workspace. If there are several solutions, then which produces the most aesthetic (good-looking) workspace? Are fewer transformers always better? Consider also the need to maintain the workspace. For the purposes of this exercise we'll assume that all methods have an equally efficient performance.

Try placing a few likely transformers into the workspace and see which might be suitable.
Which will do the job, without needing too many transformers? Would conditional attribute values work?

3) Select Methodology
On consideration, I see three likely ways to carry out this project. I call them:
l Simple Filtering
l Complex Filtering
l Conditional Values
Simple Filtering filters the data and then maps it to the required values; as such it is a two-step
process. It will require more transformers but will be simpler to understand and set up.
Complex Filtering filters the data in a single step, so no further mapping is required. It’s a onestep
process, but – because the data is being filtered – still needs more transformers than
perhaps necessary. It is moderately complex.
Conditional Values will set the values directly depending on a set of inbuilt conditions. All the
work can be done in a single transformer, so it is compact, but the setup and maintenance are
considerably more complex.
On the following pages we’ll detail how to set up each method. Pick which one you want to try
and follow the instructions. Alternatively, do each in turn – then you’ll be able to compare the
different methods and decide which you think is the best.