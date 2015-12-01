# The Generic Reader/Writer

The Generic Reader and Writer allow FME workspaces to be freed from format restrictions.

**Generic Formats**

FME’s generic tools are a Reader and Writer that are not tied to a particular format. The Generic Reader is capable of reading almost any format of data, and the Generic Writer is capable of writing almost any format of data.

In that way, a single workspace can be used to process different data formats without being specifically set up for that format.

**The Generic Reader**

Whereas all other Readers are tied to a particular format, the Generic Reader is capable of handling almost any format.

A Generic Reader is simply added the same way that any other Reader is used; by specifying the format in the new Reader dialog:

A parameter allows the format of the data being read to be specified, or it can be left up to FME to ascertain the format from the data extension of the source file.

Now at run time, the source dataset can be set to GML:

Or MapInfo TAB:

Or any other format of data you care to read (provided the data has the same schema). This makes for a very flexible workspace.

Generic Reader Feature Types

However, the Generic Reader is not immune from the Unexpected Input Remover. Remember, this is the functionality that filters incoming data against the list of feature types (layers) that are defined in the workspace. If the incoming data is stored on a layer that is not defined in the workspace, then it will be removed.

For this reason, you’ll want to ensure that all potential layers are defined as feature types in the workspace; or that you have a Merge Feature Type set in the Feature Type Properties dialog:

With that setup, any layer of data can be passed into the workspace:

**Generic Reader Parameters**

All Readers in a workspace have a number of parameters that can be used to control how that Reader operates. Each format has its own set of specialized parameters.

However, the Generic Reader has none of these.

So, for example, a user wishes to apply a particular parameter to a GML dataset read with the Generic Reader, how is it done?

In brief, the solution is to add a dummy GML Reader. In fact, a Resource Reader is the best solution, because it applies parameters without reading any data (more info on Resource Readers appears later in this chapter).

When the Generic Reader reads a dataset of GML format, it will now look to the parameters of the dummy Reader, and use those to set how it reads GML datasets.

For example, this workspace author uses a Generic Reader to read his GML data. It is a dataset of parks in the city but, sadly, the x/y axes are being read incorrectly:

There is a parameter to control the x/y axes in the GML Reader, but it doesn’t appear in the Generic Reader. So, the author selects Reader > Add Reader as Resource from the menubar:

When prompted the user defines the format as GML and picks a GML dataset (it won’t matter which).
In the Navigator window they locate the newly added Reader under Workspace Resources…

…and locates/set the GML Axis Order parameter:

Now when the workspace is run, the Generic Reader uses this GML resource to determine the parameters to read GML data with. The parameter is applied and the data read correctly:

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
“If the Input Format parameter is turned into a user parameter, then the
user can specify at runtime what format of data is being read. This is
especially helpful when the extension is – like .mdb – one used by
multiple formats.
Additionally, the workspace can be made to test for the format being read and then filter
the data to process different formats in different ways:”
</span>
</td>
</tr>
</table>