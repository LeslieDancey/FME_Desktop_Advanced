# Manual Schema Handling


For full control over how the attribute schema is handled in a custom transformer, the workspace author should create it using the setting ‘Advanced – Fix Manually’.

At that point the custom transformer has no published parameters, and therefore no userdefinable options:

To expose a parameter or attribute, the workspace author must go to the transformer definition and manually create a published parameter:

Then the parameter must be selected wherever it is going to be used:

Compared to the automatic process, in manually defined schema handling it’s more obvious – to an experienced user – what is happening. However, it’s not such an easy process for a newer user to be able to set up.

**Handling Outgoing Attributes**

Besides incoming attributes, there is also the question of what attributes should emerge from the output of a custom transformer.

Best Practice suggests that we really don’t want to output more attributes than are expected by the user.

For example, we would want to hide or remove any attributes that are part of a calculation, or any attributes that are otherwise generated inside the custom transformer but aren’t necessary to the output.

Here the custom transformer is calculating the average area of a number of polygon features.
The required output is an attribute called AverageArea.

However, no effort is being made to clear up other attributes that are being used or generated, such as _area, _min, and _max.

The workspace author should clean up this output. They can do this by visiting the custom transformer definition, clicking on the parameters (cog wheel) button for the output port object, and opening a dialog in which the attributes to be output can be defined: