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