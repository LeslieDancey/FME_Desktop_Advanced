# Schema Handling in Dynamic Translations

Dynamic Translations still use a schema, but it is not necessarily a carbon copy of the source dataset.

**Dynamic Translation Settings**

Opening the feature type properties dialog for a dynamic translation reveals the checkboxes that turns on this behavior.

For a Reader, all that is really happening is the merge feature type setting is turned on:

For a Writer, there is a special Dynamic option (it’s not just a feature type fanout):

So, it is possible to create a dynamic translation by turning one or both of these settings on manually; there’s no necessity to do so at the time the workspace is created.

The two extra parameters on the Writer are to control the source of the schema being used on the output dataset.

