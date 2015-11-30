# Custom Transformer Versioning

FME includes functionality so that any single custom transformer can exist in a number of versions.

**Why use Versioning?**

Versioning means a single custom transformer can exist in any number of versions.

One advantage of versioning a custom transformer is that you have a record of previous versions and therefore can revert to a previous one should the need arise.

However, a more important advantage relates to FME releases and new functionality.

For example, a custom transformer shared by many users could be updated to use new behaviour in FME 2015. If that custom transformer is versioned then the previous version remains available to users who have yet to update to 2015, while users who have updated to FME2015 can update their custom transformer to match.

**Creating a Versioned Custom Transformer**

Versioning can occur whenever you edit a linked custom transformer and then attempt to save it. In that situation a dialog will open to ask what you wish to do:

The two options are to overwrite the existing version or to create a new version. Creating a new version does not create a separate fmx file; instead it creates a separate version of the transformer in the same fmx file.

The title bar in Workbench also changes to illustrate that this is now a new version.

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
“Subsequent saves don’t update the version number. A new version is only
created for a new edit session; i.e. the first time you save the transformer
after it is newly opened in Workbench.”
</span>
</td>
</tr>
</table>

**Editing a Specific Transformer Version**

Whenever a versioned custom transformer is initially opened in Workbench, you are prompted as to which version you wish to edit, or whether you want to just start with a new version:

This way you are able to make edits on older versions, which is particularly useful when that version is tied to a particular FME release.

**Updating a Transformer Version**

Whenever a workspace contains a linked custom transformer, and FME detects that a new version is available, then an option appears on the context menu to allow an update to the new version:

If you have the ‘Show Transformer Version’ option turned on under Tools > FME Options > Transformers, then the tooltip will now show the transformer version:

Note that if I was using a version of FME that is incompatible with the updates in version 2, then I would not be given the option to update.

I notice that there’s a custom transformer to calculate the average area of a number of polygon features. But there’s no such transformer to calculate the average length of linear features.

Let’s fix that situation by creating such a transformer.

**1)** Open Workspace

Open the workspace C:\FMEData2015\Workspaces\DesktopAdvanced\Exercise3e-Begin.fmw.

You’ll see that the workspace is reading a set of bicycle path data, and then doing some minor processing to get it into a reasonable state for use in the workspace.

You may want to run the workspace to examine the output and see what data we are dealing with; but remember the custom transformer we will create is to be designed to work on any linear data.

**2)** Add Length Calculator

The contents of the transformer will be fairly straightforward and we’ll start out with just two transformers. So, simply add a LengthCalculator and a StatisticsCalculator transformer to the workspace.

**3)** Create Custom Transformer

Select the two newly placed transformers and turn them into a Custom Transformer called AverageLengthCalculator. Make sure the attribute references are handled automatically, although at the moment there aren’t any references to handle.

**4)** Edit Custom Transformer

Now we have a new custom transformer, let’s tidy it up and make it functional.

Firstly rename the input port object to Lines (thus identifying what geometry is expected), then add an output port object (if you don’t have one already) and rename it to Output. It should be connected to the StatisticsCalculator:Complete port:

Now open the LengthCalculator parameters. Rename the Length Attribute to _temp_length.

Then open the StatisticsCalculator parameters. Set Attributes to Analyze to _temp_length

Clean up the output attributes by removing all of them except Mean Attribute – and that one should be renamed to AverageLength

Finally, open the parameters for the Output port object. Change Attributes to Output to ‘Specified Attributes Only’ and ensure that AverageLength is output, but _temp_length is not.

If you see other attributes (such as _max) then you obviously didn’t clear them out of the StatisticsCalculator. That’s OK. Just make sure they are unchecked in this dialog.

5) Run Workspace

Run the workspace (unless you need to reattach an Inspector transformer, you don’t even have to return to the Main tab to do this). Inspect the output to ensure everything is working as expected.

6) Export Custom Transformer

Select File > Export as Custom Transformer from the menubar. In the Export as Custom Transformer dialog make sure the Insert Mode option is set to Linked by Default. Make sure the 

Save Location is the default for storing custom transformers (<user>\FME\Transformers).

Click OK to close the dialog. The custom transformer is saved (as AverageLengthCalculator.fmx) and this file opened up in a new instance of FME Workbench.

**7)** Examine Workspace

Go back to the instance of FME Workbench where the original workspace is open. The custom transformer is now a cyan color to denote that it is now a linked transformer.

Notice that you can right-click and choose to embed the transformer, and then switch back to the linked version. In a real-life scenario, which you choose would usually depend on whether you are planning to share the transformer.

In embed mode, right-click the transformer and choose Edit. Then in the definition make a small change (like moving one of the objects). Back in the Main tab you’ll find that you can no longer change back to Linked mode, because the two definitions are now different!

Delete the embedded transformer. You’ll be prompted whether you wish to delete the definition too. Click Yes, but then add a new linked version back again.

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
“It’s important to realize that the definition of an embedded custom
transformer can remain in the workspace, even if it’s not used. Sometimes
this is useful, sometimes not. You’ll be able to tell if such a definition
remains by looking in the Embedded Transformers section of the transformer gallery.”
</span>
</td>
</tr>
</table>

**8)** Examine Custom Transformer

Go back to the instance of Workbench where the fmx file is open. Move one of the objects about to activate the save button. Then save the file. Notice that you aren’t prompted to save a new version. That’s because you’re still in the same session. Any edits you make here will go towards the same version, until you close and reopen the file.

So, leaving Workbench open, close the fmx file. Then go to the start tab and select it from the recent Files list. Now it is reopened, any changes we make will go towards a new version.

**9)** Update Custom Transformer

Rather than just jiggling objects about to prove a point, let’s make a real update to this transformer. One thing we could do is filter data by geometry, so we aren’t trying to measure the length of a point feature, or similar.

So, add a GeometryFilter transformer, in front of the LengthCalculator.

Open the parameters and select Line and Arc as the geometries to filter by. Then click OK to close the dialog.

Adjust the feature mapping so that the Line and Arc ports are directed into the LengthCalculator. Add a second output port object by right-clicking on the canvas and selecting Insert Transformer Output. Call the newly placed port Rejected and connect the <Unfiltered> data to it, like so:

Now click the save button to save the custom transformer. You’ll be prompted whether you want to create a new version. Click the button labelled New Version to do so.

**10)** Update Workspace

Go back to the instance of FME Workbench where the original workspace is open. Click on the refresh button on the Transformer Gallery in order for FME to scan all custom transformers and discover the new version we’ve just created.

Now right-click on the AverageLengthCalculator custom transformer and there should be an option to upgrade to the latest version. Choose this option:

The transformer will be refreshed and updated, which you can tell by the presence of a Rejected port:

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
“If you have an fmx file by itself, you can have FME install it into the
correct folder by double-clicking on the file in a file browser.
Similarly, if you download a custom transformer from the FME Store, it will be stored in
a specific location where it will be recognized by FME Workbench.”
</span>
</td>
</tr>
</table>
