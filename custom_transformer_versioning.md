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