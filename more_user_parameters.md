# More User Parameters

There are many different types of user parameters and many different ways to make use of them.

**Types of User Parameters**

One of the key parameters when creating a user parameter is the parameter type. There are many different types, of which the more common ones are:

- Choice
- Choice with Alias
- Float
- Integer
- Text and Text (Multiline)

**Choice and Choice with Alias**

A choice parameter is when the user is presented with a fixed list of options and selects one of them. Here is a similar example to before. The user is being asked to enter their name. However, the names of all users are already known – presumably this is for a particular company’s staff – so a list of them is created:

That way, the user is prompted to select their name from a list. They don’t have to type it in manually.

A Choice with Alias parameter is the same as a Choice parameter in that the end-user gets to pick a value from a list. However, a lookup table maps the chosen entry to a value that gets provided to FME.

For example, this workspace takes incoming features and matches them to a database using an EmployeeID.

EmployeeID is provided by the end-user, but they can’t always remember their own ID number. So, the author creates a Choice with Alias user parameter.

The parameter is configured like so:

Notice that there are two fields in this configuration dialog; the display name and the actual value.

When a user selects their name from the list, then the value provided to the workspace is actually their employee ID. That way employee ID can be used as a match in the Joiner, without the end-user having to remember it!

<table style="border-spacing: 0px">
<tr>
<td style="vertical-align:middle;background-color:darkorange;border: 2px solid darkorange">
<i class="fa fa-quote-left fa-lg fa-pull-left fa-fw" style="color:white;padding-right: 12px;vertical-align:text-top"></i>
<span style="color:white;font-size:x-large;font-weight: bold;font-family:serif">Ms. Analyst says…</span>
</td>
</tr>

<tr>
<td style="border: 1px solid darkorange">
<span style="font-family:serif; font-style:italic; font-size:larger">
“Choice (Multiple) and
Choice with Alias (Multiple) are very
similar parameters (to Choice and
Choice-with-Alias), but let the enduser
select multiple values. For
example, if a manager wanted to run
reports on several employees, this is
what they could use.
Multiple values are returned space-delimited.”
</span>
</td>
</tr>
</table>

**Float and Integer Parameters**

Float and Integer parameters – as their names suggest – are simply ways for a user to enter a floating point number or an integer number.

These parameters are good examples of how FME will parse the input to ensure it matches the parameter type:

This image shows how non-numeric characters in either type, or a decimal point in the integer type, will be detected and rejected with a red-colored field.

**Text Parameters**

Text parameters are a simple way to accept plain text values into a workspace.

Text (Multiline) parameters allow the user to enter text broken over a number of lines.

There is no limitation on the characters that can be entered.

However, if you want the user to enter encoded characters, then you must use type Text (Multiline), like so:

That way FME will retain and use the actual value, here shown in the Data Inspector:

<table style="border-spacing: 0px">
<tr>
<td style="vertical-align:middle;background-color:darkorange;border: 2px solid darkorange">
<i class="fa fa-quote-left fa-lg fa-pull-left fa-fw" style="color:white;padding-right: 12px;vertical-align:text-top"></i>
<span style="color:white;font-size:x-large;font-weight: bold;font-family:serif">Ms. Analyst says…</span>
</td>
</tr>

<tr>
<td style="border: 1px solid darkorange">
<span style="font-family:serif; font-style:italic; font-size:larger">
“It’s worth being aware that not every transformer and format in FME will
handle encoded text. If you are unsure, then it’s safer to use a Text
parameter – that everything will support – rather than a Text (Multiline) parameter that
is not universally supported. Encoded text will not be handled, but the translation should
not cause an error.”
</span>
</td>
</tr>
</table>

**Linking User-FME Parameters**

It’s not just the case that a workspace author will want to apply user input to an attribute value.
In some cases the author will actually want to give the end-user control over an FME parameter.

In this scenario the author will create a user parameter, and then link it to the FME parameter.

For example, here the author has a workspace that writes Shape data:

They wish to give the end-user control over whether a spatial index is created or not

They already have a user parameter defined called WriteSpatialIndex, with choices Yes and No, however the user parameter does not do anything yet. It must be linked to the FME parameter.

The author can do this by either right-clicking the FME parameter and choosing Link to User Parameter, or they can right-click the User parameter and choose Apply To [FME Parameter].

Now the FME parameter is linked to the User Parameter, so whatever the user chooses will be applied directly to Write Spatial Index

If the author changes their mind, there is always an option to unlink the user parameter and return to direct author control:

**Creating Direct Links**

In the previous example, a user parameter was created separately and then linked to the FME parameter. However, it is possible to both create and link a parameter simultaneously.

In the Navigator window, simply right-click an existing FME parameter and choose the option to “Create User Parameter”.

This opens a dialog and automatically fills in a definition to create a new user parameter.

Click OK and the user parameter is created and automatically linked to the FME parameter.

The same can be done from within a transformer dialog, like so:

Here the workspace author is creating a user parameter linked to the Snapping Tolerance FME parameter in a Snapper transformer.

**Advantages and Disadvantages of Direct Links**

Creating a linked FME parameter directly like this has some obvious advantages, and perhaps some not-so-obvious disadvantages.

The most obvious advantage is that this is a single step process. The creation and linking of the user parameter is done in a single action.

Additionally, the parameter typing is taken care of automatically. If the FME parameter requires an integer value then a user parameter created directly from it will be automatically defined with an integer parameter. There’s no possibility of getting the wrong parameter type.

For example, the Snapper parameter in the previous screenshot, allows a floating point number, therefore it will create a user parameter of type float. No choice is provided; it will be a float automatically:

However, this also becomes a limitation too. Say, for example, the author wanted to provide a list of permitted tolerances; 0.5, 1.0, 5.0, etc. In that scenario they would have to create the user parameter separately – as type Choice – and then link it to the FME parameter manually.

Of course, the author would need to take care that the values provided by the user parameter were of a type that matched those expected by the FME parameter.

The other issue is one of persistence of the user parameter.

If a user parameter is created directly from an FME parameter on a transformer, then it is forever tied to that transformer. If the transformer is deleted, then the FME parameter will be deleted too.

However, if a user parameter is created separately, and linked manually to a transformer’s FME parameter, then it will remain in the workspace, even if the transformer is deleted.

This, of course, could be seen as a disadvantage, depending on whether you would like this behavior or not.

Here a user parameter was created automatically from a Snapper transformer parameter. If the Snapper is deleted, then the user parameter is deleted too:

**Pre-linked Parameters**

In some scenarios, user parameters are automatically created and linked to an FME parameter, without any sort of manual action by the workspace author.

For example, any time a Reader or Writer is added to a workspace, their source/destination dataset parameters are automatically turned into user parameters.

Here, a Source MapInfo TAB parameter is automatically linked to a user parameter called SourceDataset_MITAB:

This automatically occurs for parameters that are important to the end-user and that appear in nearly all workspaces.

The same thing happens to the Feature Types to Read parameter in any Reader that is added in dynamic mode:

<table style="border-spacing: 0px">
<tr>
<td style="vertical-align:middle;background-color:darkorange;border: 2px solid darkorange">
<i class="fa fa-quote-left fa-lg fa-pull-left fa-fw" style="color:white;padding-right: 12px;vertical-align:text-top"></i>
<span style="color:white;font-size:x-large;font-weight: bold;font-family:serif">Ms. Analyst says…</span>
</td>
</tr>

<tr>
<td style="border: 1px solid darkorange">
<span style="font-family:serif; font-style:italic; font-size:larger">
“If you – as the workspace author – don’t want or require the end-user to
have access to these FME parameters, then you can either delete the user
parameter, or just unlink it from the FME parameter.”
</span>
</td>
</tr>
</table>

Colleagues have purchased FME to do some data translations. However, not having taken the training course they are not confident users and would like to have their workspace made as simple as possible for them to run.

So, your task is to simplify their workspace using User Parameters, so the workspace can be run with minimal user intervention.

**1)** Start Workbench

Open the workspace C:\FMEData2015\Workspaces\DesktopAdvanced\Exercise1b-Begin.fmw.

This is the workspace created by your colleagues:

Notice that source tables are being grouped together and written to a Shape feature type. Their current method is to choose which tables to process by disabling them in the workspace. Similarly, they are setting the destination coordinate system and data encoding using Navigator parameters.

Also notice that the only annotations in the workspace are there to help the end user make edits to the workspace. Really there should be no need for that; published parameters should prompt the user instead, and that is what we will implement here.

**2)** Clean Up Auto-Created User Parameters

Open up the User Parameters section of the Navigator window. Notice how there are already user parameters for the source and destination datasets.

However, you know that the source data will never change, so that parameter is of no use. So, delete the user parameter labelled “SourceDataset_FILEGDB.”

Keep the parameter for DestDataset_SHAPE, as that can still be used to set the output location.

**3)** Create Encoding Paramete

One facet of the output that the users would like to control is the encoding of the dataset. This is achieved through a Writer parameter. However, it would be better for the users to set this as a user parameter.

Locate the Shape Writer in the Navigator window and expand the list of FME parameters.

Identify the Character Encoding parameter, right-click on it and choose Create User Parameter:

Simply click OK on the dialog that opens and a user parameter is created and linked to the FME one.

**4)** Create Coordinate System Parameter

Another requirement is an ability to set the output coordinate system.

However, if you simply publish the Writer’s coordinate system parameter – try it and see – then there will be a problem. The parameter will allow the end-user to select ANY coordinate system supported by FME.

It would be preferable if the parameter only allowed the end-user to select a coordinate system from a smaller list. For example, since the data is located in Vancouver, BC, it makes little sense for the user to be able to reproject it to NZMG (a New Zealand coordinate system).

So, locate the User Parameters in the Navigator Window, right-click and choose Add Parameter.

Set the Type to be Choice with Alias; set the Name to be CoordSysParam, and set the prompt to be Select Output Coordinate System:

Now click the […] button to the right of the Configuration setting. This opens a dialog in which to configure the parameter.

Normally we would enter values manually. However, for coordinate systems (and Reader/Writer formats) we have the option to have FME define them for us.

Click on the button labelled Import and choose Coordinate System(s):

This opens a list of coordinate systems that we wish to import as values in our user parameter.

Locate and put a checkmark in the box for the following coordinate systems:
- UTM83-10
- BCALB-83
- LL83
- CANBC-LCC

Then click OK to close this dialog. You will be returned to the configuration dialog and find that names and values have been automatically entered for these coordinate systems.

Click OK and then OK again to close the remaining dialogs and create the user parameter.

**5)** Link Coordinate System Parameter

Now we have the user's selection but we still have to apply it to the real parameter. So locate the Writer’s coordinate system parameter, right-click on it, and choose Link to User Parameter:

When prompted, select the newly created CoordSysParam and click OK to accept the selection.

**6)** Create Tables Parameter

The final task for us here is to create a way to decide which tables are going to be read. If you remember, at the moment the way your colleagues do this is by disabling various Reader feature types. However, there has to be a better method.

This is an interesting task because we want to control the source tables (Libraries, Parks, etc.) based on selection of output tables (CommunityFacilities, Environment, and Miscellaneous).
For example, we want the user to select output feature types like "Environment", which needs both "Parks" and "DrinkingFountains" Reader feature types.

Locate the Feature Types to Read parameter in the CommunityMap Reader "Features to Read" parameters (in the Navigator window).

Right-click on it and choose Create User Parameter.

A dialog will open that is already populated with a list of feature types.

Check the box that is labelled Use Alternate Display Name. This provides the ability to give alternate names for each feature type. What we need to do is use this dialog to group together common Reader feature types under a single display name.

Delete the entry for GarbageSchedule, as this data isn’t connected and is not needed.

Then, match the contents of the workspace by editing the Display Names. They should match as follows:

Underneath that change the prompt to read “Tables to Write” and then click OK to close the dialog.

**7)** Save and Run Workspace

Save the workspace. Then start up the FME Quick Translator application, located on the Start menu under the FME Desktop Utilities folder.

In there, select Run from the Getting Started menu:

Browse to the newly saved workspace, select it, and click Open. You will be presented with a list of published parameters, just as the end-user would see it:

Pick Unicode 8-bit (utf-8) as the encoding. Select a coordinate system, noting how the user is restricted to those chosen by us. Select one or two of the tables to write and click OK to run the workspace.

The translation will be carried out. Inspect the data to ensure the results are correct. The CommunityFacilities – for example – should be made up of both libraries and community centres.

***NB:** *If you run the workspace multiple times you will get multiple sets of results in the same folder! So Best Practice suggests you empty the output folder each time you run the workspace, but you can also find the latest results by checking the file dates/times.**

<table style="border-spacing: 0px">
<tr>
<td style="vertical-align:middle;background-color:darkorange;border: 2px solid darkorange">
<i class="fa fa-cogs fa-lg fa-pull-left fa-fw" style="color:white;padding-right: 12px;vertical-align:text-top"></i>
<span style="color:white;font-size:x-large;font-weight: bold;font-family:serif">Advanced Exercise</span>
</td>
</tr>

<tr>
<td style="border: 1px solid darkorange">
<span style="font-family:serif; font-style:italic; font-size:larger">
Speaking of Best Practice, don't forget to tidy up the workspace and give it a better style and structure.
</span>
</td>
</tr>
</table>