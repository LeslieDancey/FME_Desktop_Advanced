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