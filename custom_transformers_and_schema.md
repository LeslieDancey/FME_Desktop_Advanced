# Custom Transformers and Schema

Schema Handling is one of the most misunderstood components in Custom Transformers.

**Attribute Schema**

The main consequence of making a reusable custom transformer is that the author (and FME) cannot be sure where the transformer will be used and whether the schema will always match what is required.

For example, in this workspace a custom transformer carries out processing on incoming data using an attribute called AddressID as a key field.

However, if – in the same workspace – that transformer is duplicated and connected to a different Reader feature type, there is no guarantee that AddressID will exist.

For example, here it is connected to a feature type where the field is in upper case, which will cause the workspace to fail when run:

Therefore it’s vital that there is some form of mechanism for protecting against problems of a mismatched schema of this type. In fact there are two ways this can be handled: FME can automatically take care of the schema, or the workspace author can handle it manually.

**User Parameters**

The other ‘schema’ items that need to be handled are published parameters.

If an FME transformer has been set up with a published parameter, and then that FME transformer is incorporated into a custom transformer, then there needs to be a way for that user input to be passed to the custom transformer.

For example, if a transformer with these parameters is used in a custom transformer, there still needs to be a method for the user to select values for these fields:

**Automatic Schema Handling**

When a custom transformer is created, one of the parameters in the Create Custom Transformer dialog is labelled Attribute References.

If this value is set to ‘Handle with Published Parameters’ then FME will automatically take care of attribute references in the custom transformer by turning them into published parameters.
These published parameters become exposed in the parameters dialog for the custom transformer meaning they can be set wherever the transformer is used.

For example, here is a set of FME transformers for styling data as KML. In effect it is a cutdown version of the KMLDiagrammer transformer available on the FME Store.

Incoming data is basically turned into a 3D column, where the width (x and y axes) and height of the column are set by attribute values, and the color through a published parameter:

In this instance the attributes used are ParkCycleVisitors and ParkHikingVisitors (for the column x/y width) and TotalParkVisitors for the height (z axis extrusion) of the column:

The workspace author decides to turn this into a custom transformer, so he can use the same technique on other data, such as election results or planning applications. However, the question is, how can the transformer be set up to use an attribute called ElectionTurnout, when at present it is expecting TotalParkVisitors?

The answer is to use the ‘Handle with Published Parameters’ setting when creating the transformer:

Turn the above into a custom transformer and - with this new parameter set – the result is a transformer like this: