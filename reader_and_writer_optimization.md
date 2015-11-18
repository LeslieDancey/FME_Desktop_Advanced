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

Here, for example, this SQL Server Reader has a ‘WHERE Clause’ parameter that can be
applied: