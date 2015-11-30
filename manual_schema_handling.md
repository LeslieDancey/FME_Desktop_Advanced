# Manual Schema Handling


For full control over how the attribute schema is handled in a custom transformer, the workspace author should create it using the setting ‘Advanced – Fix Manually’.

At that point the custom transformer has no published parameters, and therefore no userdefinable options:

To expose a parameter or attribute, the workspace author must go to the transformer definition and manually create a published parameter:

Then the parameter must be selected wherever it is going to be used:

Compared to the automatic process, in manually defined schema handling it’s more obvious – to an experienced user – what is happening. However, it’s not such an easy process for a newer user to be able to set up.