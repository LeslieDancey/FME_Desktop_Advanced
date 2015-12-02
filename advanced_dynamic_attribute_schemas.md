# Advanced Dynamic Attribute Schemas

The attribute schema in a dynamic translation can come from a multitude of places… or none!

In general, the schema for a dynamic translation will come either from the source dataset itself, or from a different dataset (such as the database table the data is being written to).

However, there are two other scenarios for providing the output schema: it can come from a text file (or spreadsheet) in which the definition is stored; or it can be actually defined dynamically as a list of attributes in a workspace.

**Table-Based Schemas**

In this scenario, the output schema is stored as some form of table in a text file or spreadsheet; for example:

Here the author has listed a series of feature types, attributes, and geometry types that define the output schema. In FME they would use this schema by adding a Resource Reader. The format of the Resource Reader would be Schema (From Table):

In the parameters dialog for this Reader, there are parameters that specify which fields in the table represent which parts of the schema:

Geometry type is optional, but used in this example.

Attribute sequence is another optional parameter. It defines a field in the table that records the order that attributes should appear in.

Then, of course, this Reader must be used as the source for the output schema:

The incoming attributes must then be mapped to the outgoing schema. The best way here is the SchemaMapper transformer, since it too can use a lookup table to create its mappings.

<table style="border-spacing: 0px">
<tr>
<td style="vertical-align:middle;background-color:darkorange;border: 2px solid darkorange">
<i class="fa fa-quote-left fa-lg fa-pull-left fa-fw" style="color:white;padding-right: 12px;vertical-align:text-top"></i>
<span style="color:white;font-size:x-large;font-weight: bold;font-family:serif">Sister Intuitive says…</span>
</td>
</tr>

<tr>
<td style="border: 1px solid darkorange">
<span style="font-family:serif; font-style:italic; font-size:larger">
“The great advantage of this method is that you don’t need to edit the
workspace, or edit a dataset, to make schema changes.
Once you change the output schema in the table, then that is automatically applied in the
FME translation. That’s heavenly!”
</span>
</td>
</tr>
</table>

**Constructed Attribute Schemas**

This scenario is a way to construct an attribute schema using lists in FME. The schema is defined by using attributes in the list, for example:

When a feature with such attributes is sent to a dynamic Writer, then this schema is used in preference to any other.

<table style="border-spacing: 0px">
<tr>
<td style="vertical-align:middle;background-color:darkorange;border: 2px solid darkorange">
<i class="fa fa-quote-left fa-lg fa-pull-left fa-fw" style="color:white;padding-right: 12px;vertical-align:text-top"></i>
<span style="color:white;font-size:x-large;font-weight: bold;font-family:serif">Sister Intuitive says…</span>
</td>
</tr>

<tr>
<td style="border: 1px solid darkorange">
<span style="font-family:serif; font-style:italic; font-size:larger">
“The dynamic properties dialog still requires a Reader to be selected,
even if you’re not using its schema for the output. My advice is to add a
Null format Reader and use that anyway. Then you can be sure that
nothing else is being accidentally used!”
</span>
</td>
</tr>
</table>

It makes sense for this transformer to do this because it creates data in a way that we are less likely to know the schema of in advance. If you have a dynamic writer and send this data to it then the output will be in this schema.

**FME Data Types**

Both of the two preceding tools allow the user to define attribute type in an output schema.
There are a set of valid datatypes in FME, which are as follows:

- Character Fields:fme_varchar(width), fme_char(width), fme_char
- Integer Fields:fme_uint8, fme_int16, fme_uint16, fme_int32, fme_uint32, fme_int64,
fme_uint64
- Numeric Fields:fme_decimal(width,decimal), fme_real32, fme_real64
- Date-Time Fields:fme_datetime, fme_time, fme_date
- Other Fields:fme_buffer, fme_boolean

In Exercise 4d, we created a new community map dataset for the planning department using a dynamic schema. At the time only two tables were defined, but now another one is required and the planning department wants you to update the workspace.

Rather than do that, you figure that you can simply create an Excel spreadsheet containing the schema definition, so the planning team can edit it themselves and do the same for all future updates.

**1)** Inspect Spreadsheet

Open and examine the spreadsheet at:

C:\FMEData2015\Resources\CommunityMapSchema.xlsx.

If you don’t have Excel then open it in the FME Data Inspector and switch to Table View.

The table looks like this, with Firehalls, Parks, and Zones feature types defined.

**2)** Start Workbench

Open the workspace C:\FMEData2015\Workspaces\DesktopAdvanced\Exercise4e-Begin.fmw

This is the workspace you created in Exercise 4d.

**3)** Delete CommunityMap Resource Reader

We no longer need the CommunityMap Resource Reader, so locate it in the Navigator window, right-click on it, and choose Delete.
When prompted, click OK to confirm that all references relating to this dataset will also beremoved.

**4)** Add Excel File as Reader Resource

Now select Readers > Add Reader as Resource. In the dialog that opens choose:

Reader Format Schema (From Table)
Reader Dataset C:\FMEData2015\Resources\CommunityMapSchema.xlsx

Click the parameters button (if you don’t you will be prompted to anyway). This dialog is where we can define how the table maps to the required schema.

Check the Reader parameters at the top. They should show the dataset is an Excel format file.
Select Sheet1 as the table to use:

The first row should get used as the field names. If this is not the case, then click the parameters button above and set the values properly:

Next select the appropriate fields to match to the required parameters (for example Feature Type = FeatureType).

Click OK to close the dialog and again to add the Reader.

Now open the feature type properties dialog for the Writer feature type.

Under the User Attributes tab remove the LastUpdatedBy attribute, as we’ve added this to the spreadsheet definition for each type and no longer need it in here.

In the General tab click the Schema Sources edit button. Uncheck FireHalls and check CommunityMapSchema [SCHEMA_FROM_TABLE].

Click OK and OK again to close these dialogs.

**6)** Add Reader

If you noticed, the schema spreadsheet included an entry for the Zones dataset, so add a Reader (not a Resource – we really want the data this time) as follows:

Reader Format MapInfo TAB (MITAB)
Reader Dataset C:\FMEData2015\Data\Zoning\Zones.tab

Once added, connect its Reader feature type to the dynamic Writer feature type.

**7)** Save and Run Workspace

Save the workspace and then run it.

Inspect the output. Notice that all three feature types have been written, and that their attribute schema matches what was defined in the Excel spreadsheet; including the LastUpdatedBy field for each one.

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

</span>
</td>
</tr>
</table>

If you have the ability to edit the Excel spreadsheet then let’s do a couple more advanced steps (alternatively you can convert the spreadsheet to a CSV dataset and work in there).

The planning team have decided they should rename some attributes, so open the spreadsheet and rename the following for the FireHalls feature type:
- Name to HallName
- Address to HallAddress
- PhoneNumber to HallPhone

Save the spreadsheet.

If you run the workspace now it will run to completion, but there will be no values in the renamed fields. That’s because FME has no way to tell how to map the source data to the new schema.

We could simply add an AttributeRenamer transformer to handle this change, but the better way is to use the SchemaMapper. That way it can be made a little more dynamic.

In sheet 2 of the spreadsheet, enter:

OldAttrName NewAttrName
Name HallName
Address HallAddress
PhoneNumber HallPhone

Then save the spreadsheet.
Add a SchemaMapper transformer to the workspace, with both output ports connected to the output feature type.

Open the parameters dialog. For the format select the edited Excel file:

Click the parameters button. Under Sheets to Read, turn off Sheet1 and make sure Sheet2 is selected. Click OK to close the dialog.

Click the Next button. In the next dialog, select Add > Attribute Map.

When prompted, select OldAttrName as the source field and NewAttrName as the Destination field. Check the box to Remove the original attributes (i.e. this is a renaming, not copying):

Click OK to close this dialog, then click Finish. Now save and run the workspace again.

This time the output will have its attributes properly mapped. So now the planning department can translate their data, decide on the output schema, and map source to destination attributes dynamically; all by editing this one Excel spreadsheet.