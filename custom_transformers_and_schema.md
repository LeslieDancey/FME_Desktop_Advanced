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

The attributes being referenced by the custom transformer have been exposed as published parameters, so that wherever the custom transformer is used, the user has the option to select their own attributes.

They don’t have to rename their attributes to TotalParkVisitors, for example, in order to use the transformer. Also notice that the existing published parameter – Output Color – has also been exposed in this dialog, solving the second part of the schema handling conundrum.

If the user then opens the custom transformer definition and examines the Navigator Window, what they will see is as follows:

This illustrates how FME has automatically solved the attribute reference problem using published parameters. To make the custom transformer more generic, the workspace author will probably want to change the prompts on these parameters – and maybe reorder them – so they don’t refer only to the current parks scenario:

Now, when used, the custom transformer has prompts that are a lot more generic, and will make sense when it is used elsewhere:

**Post-Creation Schema Handling**

The ‘Handle with Published Parameters’ setting is available when a custom transformer is created, but there also needs to be a mechanism for handling edits to a custom transformer, or where the custom transformer is created from scratch.

This is achieved using a schema-editing button on the custom transformer.

In a custom transformer definition, notice that input ports have a cog-wheel parameters icon, just like most other canvas objects:

Clicking this button opens a dialog in which the incoming schema can be defined.

For example, here our workspace author adds a new transformer to a custom transformer definition in order to create label features:

They’ve also added a separate output port – and renamed them too – which is an excellent show of FME Best Practice!

The author would like to use the Park Name attribute (ParkName) as the content for the label.

However, they cannot do that since ParkName was not used by the custom transformer when it was created, therefore FME did not need to expose it automatically:

That attribute is literally not available inside the custom transformer definition.

The solution is to click the icon to open the Input port parameters, and expose ParkName there:


Now ParkName becomes available for use inside the custom transformer:

Additionally, back on the main canvas, the custom transformer has a newly exposed parameter ready to accept an attribute to use as the label content:

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
“Basically, published parameters are the aerodynamic solution for handling
schema inside a custom transformer. This automated behavior makes it
easier for a new user, as they can use custom transformers without having
to know about published parameters and how they operate.
Think of it as an auto-pilot for custom transformers. It’s a perfect introduction for new
users, and even experienced users will find it a nice break from flying manually.
I like to call it George!”
</span>
</td>
</tr>
</table>

Having created a custom transformer in exercises 3a and 3b, we should check that the schema is going to be handled correctly.

**1)** Start Workbench

Open the workspace C:\FMEData\Workspaces\DesktopAdvanced\Exercise3c-Begin.fmw

If you check back to exercise 3a, you’ll see that the transformer was created using the automatic schema handling parameter and the workspace will already be handling schema properly. That’s how we were able to duplicate the transformer in exercise 3b and select one of the two attributes.

**2)** Set Parameter Prompts

One issue outstanding is that the prompt used by the transformer is not very generic. Let’s fix that. Click on the tab labelled DensityEvaluator to switch the canvas to the custom transformer definition. Browse the Navigator window to find the published parameter that FME created.

Right-click on the parameter and choose Edit Definition. In the dialog that opens set the parameter prompt to: Density Attribute