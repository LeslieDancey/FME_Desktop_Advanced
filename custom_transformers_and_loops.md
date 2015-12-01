# Custom Transformers and Loops

Loops are a way to carry out a process that repeats a section of transformers.

**What is a Loop?**

A loop is a programming structure that allows an action to be repeatedly executed.

Often this is used to carry out iteration; where a process repeats to gradually narrow down the process to a desired result. Usually a loop is linked to a condition; i.e. the action continues until a certain condition is met.

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
“I often get into a loop when flying. I have to circle the airport again and
again (the action), until I have clearance to land (the condition).”
</span>
</td>
</tr>
</table>

In FME, loops are only permitted inside a custom transformer.

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
“For an excellent example of looping in an FME workspace, check out the
customer story at: www.fme.ly/LoopExample
There the user uses a loop inside to place trees (the action) until a certain density is
reached (the condition).”
</span>
</td>
</tr>
</table>

**Setting up a Custom Transformer Loop**

A loop in a custom transformer requires two components: the start and end point of the loop.

The start of the loop is identified by an Input port object. Although it can be the same input port as used for features to enter by, this does not have to be the case. For example here there is an input port for features to arrive into, and another one for the start of the loop:

If you don’t want the Loop port to appear on the transformer itself, like this:

Then you simply have to open the Input port’s parameters and ‘unpublish’ it:

The end of a loop is identified by a Loop object. You can insert one by selecting it from the canvas context menu in a custom transformer:

When you place a loop object you are asked which Input object is to be looped to:

And then the loop is complete:

Of course, in most cases the loop needs a condition to stop processing. For example you might use a Tester to test for a particular case and then continue looping on a failure but exit when the test is successful:

If you do create an infinite loop, FME won’t run forever, and will eventually stop the process.

**Loops and Custom Transformer Type**

Loops can be implemented in both embedded and linked custom transformers. However, for technical reasons, blocking – or group-based – transformers can only be used in a linked transformer.

If you attempt to create a loop inside an embedded custom transformer that includes a groupbased FME transformer, then you will receive an error message and be prompted to export the custom transformer.

A linked custom transformer has a particular parameter (in the Navigator window) called Enable Blocked Looping:

When set to Yes then other parameters are exposed to set the number of iterations and an attribute that will hold that value:

Notice how parallel processing is turned off (the parameters are removed) for custom transformers that are being looped.

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
“Generally you only use a loop to repeat an action inside it. One-off actions
should take place outside of a loop. For example, I wouldn’t put my wheels
up and down every time I circled an airport. That would be very inefficient.
I'd do it once, either before I start, or after I finish, looping”
</span>
</td>
</tr>
</table>

A colleague is trying to calculate the top ten tree species per neighborhood in the city of Vancouver. They’ve got to the point where they can merge the neighborhood and tree datasets together – and even create an FME list of the most-populous trees – but they are having problems extracting information from that list and turning it into attributes.

Having taken FME training(!) you realize this can be done using a custom transformer loop.

**1)** Open Workspace

Open the workspace C:\FMEData2015\Workspaces\DesktopAdvanced\Exercise3g-Begin.fmw.

This is as far as your colleague got. Run the workspace to see what the output is. It will take about 90 seconds to complete (if your system is slower, or you just want it to go faster, put a Sampler transformer before the StringCaseChanger, to cut down the amount of trees beingprocessed).

The output looks like this. It’s the result of the ListHistogrammer that produces a nice, sorted list of the number of tree types per neighborhood.

**NB:** To see this you must query a feature and inspect the Information Window, not the Table View.

A looping transformer is useful here because it can scan through the list, extract all of the data we need, and process it simultaneously. It's also useful because it can handle a variable number of list items; for example, if there are only 5 species of tree in a neighborhood, we only process 5 species (not 10).

**2)** Create Custom Transformer

Click anywhere on the canvas and press Ctrl+T to start creating a custom transformer. This time, because we’re using loop functionality only available in a custom transformer, we’ll create it from scratch and not define it first in the main canvas.

Call the transformer a TreeCounter or TreeIndexer and set up automatic attribute reference handling (i.e. Handle with Published Parameters).

**3)** Connect Custom Transformer

At the moment the transformer will be empty apart from an Input and Output port. However, if you open the Input port’s parameters you’ll notice there are no attributes available.

That’s because the custom transformer is not connected to anything in the main canvas.

So the first task is to temporarily switch to the main tab and connect the custom transformer, like so:

**4)** Define Inputs, Outputs, and Loop

In the custom transformer definition itself, the first task we’ll do is create the input and output ports, and define the loop we’re going to use too.

So, go to the custom transformer definition. Add a new Input object. Open its properties dialog, rename it to Loop and turn off the Publish setting (it doesn’t need to appear as a data port).

Now place a Loop object (right-click on the canvas and choose Insert Transformer Loop). When prompted, set it to loop back to the Loop input port.

**5)** Expose Attributes

We’ll need to use some attributes in here, so open the Input port parameters dialog and expose the list attributes _histogram{}.count and _histogram{}.value.