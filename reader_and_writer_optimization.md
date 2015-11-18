# Reader and Writer Optimization

There are perhaps fewer methods to improve Reader and Writer performance, but they are no less important.

**Assessing Reader Performance**

To be able to improve the efficiency of a Reader requires an estimate of how well it is working in the first instance; yet this can be hard to separate out in a workspace that is also transforming data.

The key message that signifies reading is complete is “Emptying Factory Pipeline”. Here, for example, reading of the data finished after 144 seconds of processing (of course the actual elapsed time might be longer if FME was waiting for a database or the file system to respond):

*2014-12-08 10:46:52| 144.1| 0.0|INFORM|Emptying factory pipeline*

But sometimes that number can be misleading. Take this workspace that reads a set of address points and finds their nearest neighbor in a second dataset:

According to the log file the data took 27.5 seconds to read:

*2014-12-08 13:13:52| 27.5| 0.0|INFORM|Emptying factory pipeline*

And in total the whole workspace took 27.6 seconds to run:

*INFORM|Translation was SUCCESSFUL with 0 warning(s)*

*FME Session Duration: 27.6 seconds. (CPU: 26.8 user, 0.7 system)*

But that doesn’t seem right. How could it be that the data took 27.5 seconds to read but only 0.1 seconds to process?

In fact, this is because FME was processing the data at the same time as it was reading it. It won’t read the entire dataset before processing, because that would be inefficient. So although reading didn’t finish for 27.5 seconds, during that time FME was already processing the features it had read and the 0.1 seconds is the time it took to handle the final feature and end the process.

So, how can we assess the true amount of time taken to read the data? The answer is to disable all transformation and simply run the reading part of the workspace:

Now when the workspace is run it is reading the data only, with no transformation, and the factory pipeline message appears after a mere 5.4 seconds:

*2014-12-08 13:15:12| 5.4| 0.0|INFORM|Emptying factory pipeline*

So from this we can assess that the data reading takes only 5.4 seconds out of the 27.6 total.

This is important to know to help interpret a log file and assess your Reader’s performance, particularly since the log that appears while processing would appear to be still reading data:

For example, if your processing was very complex and taking hours to complete then you might mistakenly believe the data was still being read because “Reading source feature” messages were still appearing.

**2014-12-08 13:24:54| 3.7| 2.1| INFORM| Reading source feature #5000*

**2014-12-08 13:24:58| 8.2| 4.4| INFORM| Reading source feature #5000*

*2014-12-08 13:25:03| 13.1| 4.9| INFORM| Reading source feature #10000*

...when, in fact, data was simultaneously being processed.

<table style="border-spacing: 0px">
<tr>
<td style="vertical-align:middle;background-color:darkorange;border: 2px solid darkorange">
<i class="fa fa-quote-left fa-lg fa-pull-left fa-fw" style="color:white;padding-right: 12px;vertical-align:text-top"></i>
<span style="color:white;font-size:x-large;font-weight: bold;font-family:serif">Jake Speedie says…</span>
</td>
</tr>

<tr>
<td style="border: 1px solid darkorange">
<span style="font-family:serif; font-style:italic; font-size:larger">
“Not to confuse matters, but the exact structure of the log will depend
greatly on whether the transformers being used are feature-based or
group-based.
Remember, a group-based transformer will hoard features until it is ready to process
them all, and this will look very different in the log to a feature-based transformer that
processes features one at a time.”
</span>
</td>
</tr>
</table>

**Improving Reader Performance**

One obvious way to improve reading performance is to upgrade the underlying system to minimize the amount of time FME spends waiting for a response.

For example, here approximately 12% of the translation (0.4 seconds) was spent waiting for the system to return the requested data:

FME Session Duration: 3.1 seconds. (CPU: 2.6s user, 0.4s system)

Here the delay is not particularly problematic; but with larger amounts of data, and perhaps reading from a remote database server, the time taken could be more important.

The second obvious way to improve reading performance is to minimize the amount of data that is being read. For example, this workspace reads nearly 14,000 features, but immediately discards all except 132 of them:

In this scenario, and where possible, it would be much more efficient to simply just read those three features.

<table style="border-spacing: 0px">
<tr>
<td style="vertical-align:middle;background-color:darkorange;border: 2px solid darkorange">
<i class="fa fa-quote-left fa-lg fa-pull-left fa-fw" style="color:white;padding-right: 12px;vertical-align:text-top"></i>
<span style="color:white;font-size:x-large;font-weight: bold;font-family:serif">Jake Speedie says…</span>
</td>
</tr>

<tr>
<td style="border: 1px solid darkorange">
<span style="font-family:serif; font-style:italic; font-size:larger">
“How sensible is it, to go into a restaurant and order the entire menu,
when you only intend to eat some of the dishes? Ordering is quicker, but
way longer to be delivered, and it will certainly be more expensive!
The same applies reading data with FME. If you read the entire contents of a dataset,
when you only need a part of that data, then you’re wasting resources and slowing down
the process. Not to mention putting stress on the CPU (Chef Processing Unit)”
</span>
</td>
</tr>
</table>

All formats have various sets of parameters that speed up feature reading by filtering the amount of data being read.

The first of these – search envelope – define the data to read as a geographic area. Then only that area of data needs to be read. Envelope parameters are found under the Advanced Parameters section in the Navigator:

These parameters are available on every spatial data Reader, but have the most effect when the source data is spatially indexed. Then the query is being carried out at its most efficient.

Similarly, there are a number of parameters designed to let the user define how many features to read. These appear in a section of parameters caled Features to Read:

These parameters include the ability to define a maximum number of features to read, and what feature to start at. There is also a parameter that defines which feature types (layers or tables) should be read.

By using these judiciously, the amount of data being read can be reduced and the translation sped up.

Other formats – particularly databases – have additional clauses that can help reduce the data flow.

Here, for example, this SQL Server Reader has a ‘WHERE Clause’ parameter that can be applied:

Using this parameter is way more efficient than reading the entire contents of a large table and using a Tester transformer in the workspace.

In short, when you want to filter source data, and can use a specific Reader parameter to do so, it is more efficient than reading all of the source data and then filtering it with a transformer.

<table style="border-spacing: 0px">
<tr>
<td style="vertical-align:middle;background-color:darkorange;border: 2px solid darkorange">
<i class="fa fa-quote-left fa-lg fa-pull-left fa-fw" style="color:white;padding-right: 12px;vertical-align:text-top"></i>
<span style="color:white;font-size:x-large;font-weight: bold;font-family:serif">Jake Speedie says…</span>
</td>
</tr>

<tr>
<td style="border: 1px solid darkorange">
<span style="font-family:serif; font-style:italic; font-size:larger">
“Quick reading tip for CSV data.
Use the PointCloud XYZ format to read CSV data, then the
PointCloudCoercer transformer to turn it into points. It works way faster than just using
the CSV format!”
</span>
</td>
</tr>
</table>

There are two other Reader scenarios to avoid, as they can cause performance degradation.

Firstly – specifically for formats with a table list – there is the case where you have more feature types than are necessary.

Here the user has added a number of tables to their PostGIS database Reader:

 
However, if you look at the workspace, many of these tables are not even connected to anything. The unconnected tables are still being read but the data is being ignored:

Basically, if you don’t need the data, and the feature type is not connected to anything in the workspace, then delete that feature type.

Then the table will not be read and performance will improve.

The second scenario – specifically for file datasets – is a "dangling" Reader. This is where you have deleted all of the feature types, but not the underlying Reader:

Here the user set up a Reader to read an AutoCAD dataset. The feature type (layer) definitions were deleted from the workspace, but the Reader remains.

When the workspace is run, all the data is still being read from this file, but then discarded as "unexpected input."

Remember, any extra data that is read – of whatever amount – takes time and resources to read, and if it subsequently goes into the workspace, will slow it unnecessarily too.

**Assessing Writer Performance**

Assessing the speed of writing can be similarly difficult to assessing the speed of reading; again the reason is the same: FME starts writing data as soon as it becomes available, and doesn’t necessarily wait until processing is done.

Take the previous workspace, which read a set of address points and found their nearest neighbor, but now has a Writer too:

According to the log file, we find that the output dataset is open for writing before the source dataset has even finished being read!

Opened Shape File C:\FMEData2015\Output\PostalAddress.shp for output

Opened DBF File 'C:\FMEData2015\Output\PostalAddress.dbf' for output

DBF Writer: Writing DBF File using character encoding 'ANSI'

Reading source feature # 5000
Reading source feature # 7500
Reading source feature # 10000
Reading source feature # 12500

Plainly it’s harder to isolate the Writers to check how fast they are operating; you can’t just disable everything else in the workspace without preventing anything from happening.

However, it can be done with a two-step process. Firstly you would add a Recorder transformer – after all other transformation has taken place – to preserve the data in FFS format at the moment it is about to be written:

Now replace the Recorder with a Player transformer – to re-read the preserved FFS data – and disable everything else up to that point.

Now the data will be played back into the workspace, and is followed up by being written to the output.

In this example the "Emptying Factory Pipeline" message appeared after 7.2 seconds and the translation took 8.9 seconds in total, indicating 1.7 seconds was spent writing data.

<table style="border-spacing: 0px">
<tr>
<td style="vertical-align:middle;background-color:darkorange;border: 2px solid darkorange">
<i class="fa fa-quote-left fa-lg fa-pull-left fa-fw" style="color:white;padding-right: 12px;vertical-align:text-top"></i>
<span style="color:white;font-size:x-large;font-weight: bold;font-family:serif">Jake Speedie says…</span>
</td>
</tr>

<tr>
<td style="border: 1px solid darkorange">
<span style="font-family:serif; font-style:italic; font-size:larger">
“Be aware that fanouts will complicate your view of the log, not to
mention slow the process somewhat.
For example, if I do a Dataset Fanout on the above workspace, FME creates a separate
Writer for each fanned-out dataset.
Firstly this causes a performance hit – because FME has to cache all the output data and
create multiple Writers – and additionally I get a section of log for each output dataset.”
</span>
</td>
</tr>
</table>

**Improving Writer Performance**

Again, the most obvious way to improve writing performance is to upgrade the underlying system to minimize the amount of time FME spends waiting for a response.

If you are writing to a file system then make sure the disk is fast and responsive – use solid state drives – and that the operating system is not busy writing other files at the same time, as the latter could cause a significant bottleneck. Also check if you are using RAID as some configurations need multiple writes and can definitely slow things down.

If you are writing to a database, then existing indexes and joins can cause the process to be slower than expected. In many cases it will be quicker to drop an index, write the data, and then recreate the index. More information on database performance with FME comes in a later section.

However, the main tip for improving Writer performance is for the scenario where a workspace has multiple Writers. In this case it’s important to get the writers into the optimum order.

Each Writer is listed in the Navigator window in Workbench. The key is to ensure that the Writer that is to receive the largest amount of data is at the top of the list.

Writers can be re-ordered by moving them up and down in the list in the Navigator window, using the context (right-click) menu, like so:

Alternatively, they can be simply dragged up and down with the mouse cursor.

The reasoning behind this is that the first Writer in a workspace starts to write data as soon as it is received. Other writers cache theirs until they are ready to start writing.

Therefore, if the largest amount of data is written immediately, lesser amounts of data have to be written to, and stored in, a cache.

This can improve performance tremendously, particularly when the translation is especially unbalanced; for example one million features go to one Writer, and only ten features go to another.

For more information see the FME Evangelist article at: http://fme.ly/FirstWriter.

<table style="border-spacing: 0px">
<tr>
<td style="vertical-align:middle;background-color:darkorange;border: 2px solid darkorange">
<i class="fa fa-quote-left fa-lg fa-pull-left fa-fw" style="color:white;padding-right: 12px;vertical-align:text-top"></i>
<span style="color:white;font-size:x-large;font-weight: bold;font-family:serif">Jake Speedie says…</span>
</td>
</tr>

<tr>
<td style="border: 1px solid darkorange">
<span style="font-family:serif; font-style:italic; font-size:larger">
“Think of it like an airport. It’s more
efficient when you load the busiest flights
first, because it empties the terminal waiting areas
quicker.”
</span>
</td>
</tr>
</table>

Let’s continue to work on the workspace that processes a dataset of cell phone signals.
Remember, because of different specifications, your experience may be greatly different to what is described here.

Now we’ve deconstructed the log, let’s start to clean up any performance issues with the Readers and Writers.

**1)** Start Workbench

Open the workspace C:\FMEData2015\Workspaces\DesktopAdvanced\Exercise2b-Begin.fmw
(or stick with Exercise2a-Begin.fmw if you have it open – it’s the same workspace).

The first thing we should do is ensure we’re logging all the required timestamps. So select Tools > FME Options from the menubar in Workbench.

Click on the Runtime icon. Ensure that the Log File Defaults has “Log timestamp information” turned on.

Since the workspace doesn’t fail – it’s just a little slow – we aren’t debugging anything so you can turn off “Log debugging information” (assuming it was already turned on).

**2)** Assess Readers

Let’s first assess how well the Readers are doing their job. It might be that they aren’t really the bottleneck in our workspace.

First check the original log file for the Emptying Factory Pipeline message.

*2014-12-08 10:48:28| 60.2| 0.0|INFORM|MULTI_READER(MULTI_READER): Done reading 872554 features from 3 readers*

*2014-12-08 10:48:28| 60.2| 0.0|INFORM|Emptying factory pipeline*

It occurs after 60.2 seconds, about 25% of the total translation time. But let’s see if that’s accurate.

Select all of the objects after the feature types (i.e. transformers and Writer feature types).

Press Ctrl+E to disable them (Ctrl+E is a toggle to Enable/Disable)

The workspace now looks like this:

Run the workspace. The data will be read, but not processed or written.

Check the time taken to do this. On my machine the result is this:

*INFORM|FME Session Duration: 45.3 seconds. (CPU: 37.9s user, 0.4s system)*

*INFORM|END - ProcessID: 97468, peak process memory usage: 85344 kB, current process memory usage: 83164 kB*

So it’s actually a little quicker than the full translation suggests – not surprisingly FME is starting to process that data as it is being read. Still, we might improve on that somehow.

**3) **Check Data Filtering

The workspace is filtering data with a Tester. Is there any way that we could improve on our reading time by carrying out this test directly on the source data?

Firstly, we want all the data spatially, so there’s no use in setting any Search Envelope parameters. In any case the CSV data is not – initially – spatial and has no such parameters.

Secondly, could we apply that test to the data as it is being read? Well, neither Reader has a WHERE clause field, as neither is a database. The CSV Reader does have filter parameters, but they are regular expressions for text fields, and it would be difficult to filter on a number:

**4)** Check Other Reader Issues - 1

Are there any other issues with the Readers that might be slowing performance? Yes, there are!

Firstly, notice that the KML Reader that is reading the neighborhood data also includes a whole number of feature types that we aren’t interested in.

The only feature type we need is Neighborhoods, and that’s already connected into the Clipper transformer.

All the other feature types are producing data we don’t need. They might not be slowing us much, but they certainly won’t be speeding up the translation.

So, we should select all unconnected feature types on the canvas and delete them. The quickest way to do this is select Tools > Remove Unattached from the menubar and click OK.

**5)** Check Other Reader Issues - 2

Another oddity with our Readers is that there are three listed in the Navigator window, but only two used on the canvas.

The Addresses [FILEGDB] Reader seems to be reading data that we don’t want and don’t use.
It’s what I call a “dangling” Reader, one without feature types. Expand the Reader in the Navigator window to prove that there are no feature types.

Having satisfied yourself of that fact, click on the Reader and press the delete key to remove it.
Now run the workspace again to see if reading is any quicker.

*INFORM|FME Session Duration: 38.2 seconds. (CPU: 37.0s user, 0.4s system)*

*INFORM|END - ProcessID: 88220, peak process memory usage: 80740 kB, current process memory usage: 78560 kB*

On my computer it shaves about 7 seconds (15%) of the time off reading, which is a good start.

**6)** Check Writer Performance

We won’t check the time being taken to write the data, just look for the only obvious improvement: the order of the Writers.

As mentioned, the best way to improve Writer performance is to ensure the Writer receiving the largest amount of data appears first in the Navigator window.

In this workspace there are two Writers. One writes the problem (ColdSpot) locations. The other writes the good locations:

OK, the Writer with the most features is not currently top of the Writers list. Let’s fix that.

Right-click on the GoodLocations Writer in the Navigator window and choose the option Move Up.

Now that Writer should appear above the other in the Navigator:

Re-enable any components of the workspace that were disabled, and run the full translation again. Remember, the original log reports the following results:

*INFORM|FME Session Duration: 4 minutes 1.0 seconds. (CPU: 185.7s user, 50.4s system)*

*INFORM|END - ProcessID: 96656, peak process memory usage: 3065096 kB*

Now, on my computer, I get the following:

*INFORM|FME Session Duration: 2 minutes 44.1 seconds. (CPU: 151.9s user, 8.9s system)*

*INFORM|END - ProcessID: 98972, peak process memory usage: 1734748 kB*

That’s way better. I’ve reduced the time taken by 40% from the original. Additionally, peak memory use has dropped by 50%!

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
In FME2015 there is a new workspace parameter called "Order Writers By" that will
let you adjust the order in which Writers are initialized; either by the order of
Writers in the Navigator (as described here) or by the order features arrive at the
Writers.
</span>
</td>
</tr>
</table>
