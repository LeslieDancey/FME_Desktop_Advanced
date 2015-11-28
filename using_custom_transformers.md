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