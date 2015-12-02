# Dynamic Translations

Dynamic Translations are a way to create ‘schema-less’ workspaces.

**What are Dynamic Translations?**

In previous chapters all translations have involved a schema being defined within the workspace. In other words, the source and destination schema reflect the structure of the source data (what we have) and the destination data the user requires (what we want).

The layout of a dynamic translation does not reflect either the source or destination schema. It’s a universal layout that is designed to handle data regardless of what schema is being used.

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
“For this section it’s useful to think of a schema being comprised of a
trinity of objects: feature types, attributes, and geometry type.”
</span>
</td>
</tr>
</table>

On the Reader side of things, a dynamic workspace is very similar to using Merge Parameters; feature types are given free entry to a workspace, regardless of whether they are yet defined in there.
Data is also read regardless of attributes and/or geometry type.