# Custom Transformer Types

Custom Transformers come in two flavors: Embedded and Linked.

**Custom Transformer Types**

There are two types of custom transformers: Embedded and Linked.

An embedded transformer is one that exists only in the workspace itself. Its definition is stored (embedded) inside the workspace file and it is not available to any other workspace.

A linked transformer is one that exists outside of a workspace. Its definition is stored in its own file and it is available to any other workspace, which reference it through a link.

On a workspace canvas, embedded transformers are identified by their green color, while linked transformers are colored cyan:

**Linked vs Embedded Transformers**

Both type of transformer can be used in an FME workspace, and there are various advantages and disadvantages to each type.

**Embedded Transformers**

Embedded transformers are perhaps easier to understand and have the advantage of needing no external files, as their definition is embedded into the workspace. However, an embedded transformer cannot easily be shared with other users, unless they are given a copy of the same workspace, and it is not easy to maintain a consistent definition among several users.

**Linked Transformers**

As a separate file, linked transformers are perhaps a little harder to understand and manage.
However, a linked custom transformer is much easier to share among users: any number of users can use the same custom transformer definition. Additionally, maintenance is easier too because any changes made to the definition are automatically propagated to any workspace that uses it.

**Exporting a Custom Transformer**

All custom transformers start out as an embedded version. To create a linked version the custom transformer is exported from the workspace.

This is easily done by clicking on the canvas tab for the embedded definition and choosing File
- Export as Custom Transformer from the menubar:

At this point a dialog opens in which you can confirm the transformer name and category, plus some other parameters including the save location:

Clicking OK creates the custom transformer and opens it in a new instance of Workbench.

**Save Location**

FME has a specific installation folder in which custom transformer files can be saved. If a custom transformer is saved in this folder then it becomes available in Workbench and can be used the same as any other transformer.

When a linked transformer shows up in the transformer gallery – or Quick Add dialog – then it has a special icon to signify that you are about to use a linked version, rather than the embedded.

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
“Note the refresh button on the transformer gallery. If a custom
transformer doesn’t show up when you expect, refreshing the gallery
contents may help to locate it.”
</span>
</td>
</tr>
</table>

**Insertion Mode**

When exporting a custom transformer, the Insert Mode parameter specifies how the custom transformer can be used. There are four different modes.

If a “by Default” option is used, then any instance of this transformer that is placed can be switched back and forth from embedded to linked.

If an “Always” option is used, then any instance of this transformer is fixed in either embedded or linked mode, and cannot be switched.

**Which Mode to Use**

When an author creates a custom transformer for a customer or user who is inexperienced in FME, then Embedded Always is a good choice, since it is easier to manage (no external files) and the user cannot accidentally change it.