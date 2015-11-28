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