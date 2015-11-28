# Custom Transformers

Custom Transformers are very powerful tools at either a basic or an advanced level.

**What is a Custom Transformer?**

A custom transformer is a sequence of standard transformers condensed into a single transformer. Any existing sequence of transformers can be turned into a custom transformer.

Custom Transformer Purposes

Among other functions, custom transformers help to:

- Tidy Workspaces

By condensing chunks of content the workspace canvas becomes less cluttered

- Reuse Content

By encapsulating a sequence of transformers in a single object, they can be reused throughout a workspace and shared with colleagues.

- Employ Advanced Functionality

Using a Custom Transformer enables additional functionality to be used, such as looping and parallel processing

<!--Person X Says Section-->

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
‘Welcome aboard this Safe Software training chapter on Custom
Transformers. I’ll be your guide to all of the functionality involved.
As you can see, Custom Transformers are excellent tools for carrying out Best Practices
in FME, both speeding up your projects and reducing turbulence in the Workbench
canvas.”
</span>
</td>
</tr>
</table>

**Creating a Custom Transformer**

Custom transformers are created by either selecting Create Custom Transformer from the canvas context (right-click) menu, or by selecting Transformers > Create Custom Transformer from the menubar.

The shortcut key for this function is Ctrl+T.

A Custom Transformer can be created from scratch – i.e. you start with an empty custom transformer and add content into it – or can be created from an existing sequence of transformers.

If a number of existing transformers are selected when you issue the Create Custom Transformer command, then they are automatically added to the new custom transformer; otherwise the new custom transformer is created empty except for an input and output port.

Here a user is creating a new custom transformer based on a series of existing ones.

The new custom transformer will be pre-populated with these three raster-based transformers.

<table style="border-spacing: 0px">
<tr>
<td style="vertical-align:middle;background-color:darkorange;border: 2px solid darkorange">
<i class="fa fa-bolt fa-lg fa-pull-left fa-fw" style="color:white;padding-right: 12px;vertical-align:text-top"></i>
<span style="color:white;font-size:x-large;font-weight: bold;font-family:serif">NEW</span>
</td>
</tr>

<tr>
<td style="border: 1px solid darkorange">
<span style="font-family:serif; font-style:italic; font-size:larger">
In FME2015 the FeatureReader transformer adds raster functionality and so
replaces the RasterReader transformer.
</span>
</td>
</tr>
</table>

**Naming a Custom Transformer**

All Custom Transformers require a name and (optionally) a category and description. A dialog in which to define these automatically appears when you create a new custom transformer.

The category can be set to match any existing category of FME transformers, or a custom category of your own.

Notice also the “Use Extended Description” parameter. This allows you to enter extra information about the custom transformer, such as requirements for use, development history, and legal terms and conditions; in fields that support the use of rich text.

These fields are particularly important when you intend to share the custom transformer with work colleagues or clients.

**The New Custom Transformer**

A newly created custom transformer then looks like this:

Notice that it appears under a new tab on the Workbench canvas and consists of the three original transformers with additional input and output objects.

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
‘If the custom transformer had been created from scratch, without any
original transformers, it would look like this:
</span>
</td>
</tr>
</table>

In the Navigator window, where a workspace would have a section labelled Workspace Properties, a custom transformer has Transformer Properties.

This is where the information – name, category, description, etc. – that was entered earlier can be edited.

When you click on the Main tab, to return to the main canvas view, the three original transformers have now been replaced by a custom transformer object that is automatically connected into the existing workspace:

This custom transformer looks and behaves in the same way as any standard FME transformer; with input and output ports (that match the input/output objects in the custom transformer tab), plus a parameters dialog.

The scenario for this exercise is that an FME user has a workspace that calculates the population density for neighborhoods in the city of Vancouver. Having just found out about custom transformers, the user thinks this would be a good workspace to turn into a general solution: a custom transformer that calculates the average density of items in a known space.

**1)** Start Workbench

Open the workspace 

C:\FMEData2015\Workspaces\DesktopAdvanced\Exercise3a-Begin.fmw.

You may wish to run the workspace and examine the output to see what it does and how it works.

**2)** Create Custom Transformer

The key components for the custom transformer are the AreaCalculator and ExpressionEvaluator transformers. If you examine the workspace you’ll see two ExpressionEvaluators (one for the year 2001, one for 2011) but we don’t need to include both in the custom transformer.

So select the AreaCalculator transformer and the first ExpressionEvaluator, right-click on them, and choose the context menu option 'Create Custom Transformer.'

In the Create Custom Transformer dialog enter a name, category, and description for the new custom transformer. A good name for the transformer will be the DensityEvaluator.

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
‘You can’t call it the DensityCalculator; FME already has one of those!’
</span>
</td>
</tr>
</table>