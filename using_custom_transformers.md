# Using Custom Transformers

Custom Transformers aren’t just for tidying a workspace, but also as a way of re-using content.

**Re-Using a Custom Transformer**

Once a custom transformer has been created, its definition is stored in the workspace and can be used any number of times within that workspace.

In fact, a custom transformer that has been created can be placed into the workspace just as any other FME transformer, either through the Transformer Gallery, or by using Quick Add.

Custom transformers can be found in the Transformer Gallery window under a section labelled “Embedded Transformers."

The transformer name, category, and description all appear in the Quick Add tool, so it is definitely worthwhile setting these parameters.

Newly placed instances of a custom transformer will be renamed (or numbered) as necessary, in order to avoid a clash of names.

Editing a Custom Transformer

When custom transformers are reused like this, a key benefit for maintenance purposes is that every instance can be updated or edited simply by editing the custom transformer definition.

Custom transformer definitions are edited by clicking the appropriate canvas tab and making whatever changes are required, just as changes are made on the main canvas.

For example, if the Interpolation parameter is changed for the RasterMosaicker inside this custom transformer, then the parameter automatically changes for all instances of the transformer that have been placed.

This makes the editing of a sequence of transformers much easier, because the edit only needs to be made once; no matter how many times that sequence has been used.

**Custom Transformer Input/Output Ports**

The input and output ports on a custom transformer are defined by input/output objects in the custom transformer definition itself.

Firstly, these input/output objects can be renamed, in order that the transformer ports get named appropriately. You can either double-click the object, choose Rename from the context menu, or press F2, in order to rename the object.

For example, here the user is renaming an input port from FeatureReader_Initiator to simply Raster.

Renaming the input and output ports is useful for making the custom transformer object more legible, and for helping the user to understand what data is supposed to connect to the port.

For example, after editing the transformer might look like this:

Besides renaming ports, it is also possible to add new ports to a custom transformer.

To do so simply click the tab to display the custom transformer’s definition and select Transformer Input (or Output) from either the canvas context (right-click) menu or the menubar.

For example, here a user has added a new input port to handle vector data.

This means that each instance of the custom transformer in the main canvas will now have an extra input port, like so:

<table style="border-spacing: 0px">
<tr>
<td style="vertical-align:middle;background-color:darkorange;border: 2px solid darkorange">
<i class="fa fa-quote-left fa-lg fa-pull-left fa-fw" style="color:white;padding-right: 12px;vertical-align:text-top"></i>
<span style="color:white;font-size:x-large;font-weight: bold;font-family:serif">First Officer Transformer says…</span>
</td>
</tr>

<tr>
<td style="border: 1px solid darkorange">
<span style="font-family:serif; font-style:italic; font-size:larger">
‘To arrange the ports in a set order, change their position in the custom
transformer definition. The port that appears highest up in the canvas will
appear first on the custom transformer itself!”
</span>
</td>
</tr>
</table>

Having created a custom transformer in exercise 3a, we can now go on to make use of it multiple times and maybe even apply some edits.

**1)** Start Workbench

Open the workspace C:\FMEData2015\Workspaces\DesktopAdvanced\Exercise3b-Begin.fmw

**2)** Duplicate Custom Transformer

Notice that we have one instance of the custom transformer, that is calculating population density, but it could be used a second time in place of the ExpressionEvaluator.

Click on the ExpressionEvaluator and press the delete key to delete it.

Click on the DensityEvaluator custom transformer and press Ctrl+D (or right-click > duplicate) to create a duplicate copy of it. This is the same effect as placing a new instance, but quicker.
You could do the same task through Quick Add or the Transformer Gallery if you desired.

Connect the second DensityEvaluator into the workflow, in parallel and not in series:

**3)** Set Custom Transformer Parameters

Click the cog wheel icon to open the parameters dialog for the second DensityEvaluator. This time set the population parameter to TotalPopulation2011 (not 2001).

**4)** Run Workspace

Run the workspace and inspect the output to ensure the data is being processed correctly.

**5)** Edit Custom Transformer

One obvious problem with the output from the transformer is that the result is put into an attribute called PopulationDensity2001, regardless of what data is being processed. This is not useful; for example the 2011 results also get the same name.

We can fix this by making the output name more generic. This is good practice for a custom transformer that might be used in multiple scenarios.

Click on the tab labelled DensityEvaluator to switch the canvas to the custom transformer definition. Open the ExpressionEvaluator parameters and change the name of the Destination Attribute parameter to DensityResult.

If you run the workspace again you’ll notice that DensityResult is the attribute output by both instances of the custom transformer; i.e. one edit has fixed both of them!

**6)** Rename Ports

One other edit we ought to make is to the port names of the custom transformer. At the moment they are not very elegant.