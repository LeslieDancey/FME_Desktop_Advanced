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

**The Generic Writer**

Similarly to the Generic Reader, the Generic Writer is a component of FME without a specific format.

A Generic Writer is simply added the same way that any other Writer is used; by specifying the format in the new Writer dialog:

When a workspace with a Generic Writer is run, the format of data written is determined by a parameter that can be set in the Navigator window:

This parameter is one of those that FME automatically creates a linked user parameter for.
That way the end-user can choose at runtime which format to write to.

The Destination Dataset parameter, like all dataset parameters, is also linked to a user parameter. Note that the destination for this writer is always a folder, even when the selected format is file-based.

For example, here the user is reading a parks dataset (coincidentally also using the Generic Reader) and writing the data out to KML format using the Generic Writer:

**Semantic Translations and the Generic Writer**

It’s important to remember that FME is a semantic translator, carrying out transformations on output data to fit the definitions and rules of the destination format.

In other words, FME will automatically restructure data to fit the output format’s rules on geometry and attributes (both names and values).

Therefore, the Generic Writer may produce slightly different results for different data formats.

**Generic Writer Feature Types**

The feature types defined for a Generic Writer are – like the Generic Reader – relatively inflexible. The layers that are defined will be the layers that are created, regardless of format.

Of course, there is a way to be more flexible – and creative – with the feature types that are written, and that’s with functionality that we just covered: Fanouts!

If the Generic Writer uses a feature type fanout, based on the format attribute fme_feature_ type, then the destination dataset will have the same layers as the source – even if that varies from translation to translation!

Generic Writer Parameters

Like the Generic Reader, a particular output format in the Generic Writer can be controlled using parameters from a dummy Writer of the same format, which has been added to the workspace.

The difference is that this will be a “real” Writer and not a Resource Writer (of which there is no such thing). The dummy Writer does not need to have any feature types defined, or any data sent to it; in fact it should not as this would only slow the translation.

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
“Generic Readers and Writers by nature only deal with a flexible format,
but can also be set up to be flexible with layers.
However, each dataset being read must have the same attribute schema, and each
dataset being written will end up with the same attribute schema. This part is not
flexible.
To work with flexible attribute schemas requires the use of either Automatic Attribute
Definitions or a Dynamic Translation.”
</span>
</td>
</tr>
</table>

In this exercise your task is to create a workspace with which end-users can output a dataset of Community Mapping in a format of their choice. This would be an excellent workspace to use for an FME Server Data Download service.

**1)** Start Workbench

Start FME Workbench and begin with an empty canvas. Select Readers > Add Reader from the menubar and add the following:

Reader Format: Esri Geodatabase (File Geodb API) Reader Dataset: C:\FMEData2015\Data\CommunityMapping\CommunityMap.gdb

Workflow Options: Single Merged Feature Type

By selecting the single merged feature type option we will have a workspace that is nice and compact, plus it will allow the user to select which tables they want to read from the source.

Click OK to close the dialog and add the Reader.

**2)** Add Writer

Select Writers > Add Writer from the menubar and add a Generic Writer.

You don’t have to select an output location, but will you have to open the parameters dialog and set an original output format; so do that and select a format like Esri Shape.

In the "Add Feature Types" section of the dialog, select Automatic for feature type definitions:

In the Feature Type Properties dialog set the Allowed Geometries field to fme_any. This will allow any data to be written to this feature type. The "output" part of the Writer refers to the output location, which may or may not be set in your workspace.

Check the User Attributes tab and you will see that the attribute definition is set to Automatic.

Click OK to close the dialog and add the new feature type. Connect it to the source feature type. When you make the connection the attribute schema will automatically be updated to match the connected Reader feature type:

**3)** Check User Parameters

Look in the Navigator window at the user parameters that were created automatically with the Reader and Writer.

The parameter for source dataset we don’t need (it will always be this dataset) so delete it.

Another parameter is Feature Types to Read. This is very useful because when the user runs the workspace they will be prompted which tables to read from the source Geodatabase, so keep this one.

Similarly keep the Destination Dataset parameter.

The Output Format parameter is interesting. Double-click on it as if you were going to set a value. Notice that the "More Formats..." option in the drop-down list opens up the full FME formats list.