# Log File Interpretation


If you can’t understand what FME is doing then there isn’t much chance you’ll be able to improve upon it.

The FME log file is your best friend for assessing performance. It tells you how long a translation took, where the time went, and how well FME was able to use the available system resources.

**Deconstructing a Log File**

The first thing to notice is that the log is made up of a number of messages, each of which consists of a number of fields:
- Absolute Date [Optional]
- Absolute Time [Optional]
- Cumulative Time (for translation)
- Elapsed Time (for this message)
- Message Type
- Message

We’ll look at the time fields later. The Message Type field will be one of the following:
- ERROR: An error in the translation that usually requires FME to terminate processing.
- WARN: A warning that signifies a problem that is not sufficient to terminate processing.
- INFORM: An information message relating a non-error item.
- STAT: A message on translation statistics such as the number of features processed.

The overall structure of an FME log is basically four different sections.

- Command-line statement
- Configuration and setup information
- The translation and transformation itself
- A summary of the translation

**Command-Line Statement**

At the very top of a log file appears the command-line statement. This is the command that FME Workbench is using to run the translation.

In terms of performance, this section doesn’t tell us much. However, it is useful to confirm what FME version is running. Also, if you wanted to run the translation through the commandline, this is the statement that you’d use.

**Configuration and Setup Information**

This part of the log file tells us vital information about FME’s version and configuration, the system resources and how FME intends to use them, and what system paths are being used.

For example, here you can see which version of FME is being used, its license type, and the machine name. If you do have multiple FME versions installed, here’s where you can check to ensure the correct one is running.

Further on we can see that the system has nearly 108GB of free space and 4 GB of virtual memory (the maximum possible on 32-bit). We can also see what operating system we are running FME on and what the current language and encoding settings are:

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
In FME2015 measurements of disk and memory are now given in the most appropriate units,
quite often GB and TB, rather than MB.
</span>
</td>
</tr>
</table>

Then comes important information about the system resources and FME’s memory management:

In this case there is a limit of 4GB memory per process, indicative of 32-bit processing, out of 24GB of total memory for the machine. The following numbers indicate how FME will manage memory resources. It will use nearly 3GB of memory and then it will start to release memory by caching features to disk. This caching will stop once memory use is less than about 2GB.

This way FME will perform to its potential automatically, while not taking so much memory that the system may fail or other processes on the system would suffer.

Of course, when run on 64-bit FME, the numbers will be slightly different, illustrating the benefits of this platform:

**Translation and Transformation Statements**

The main body of the log file concerns the translation and transformation of data. This section often appears confusing to new users, until they understand how FME operates.

Firstly, there can be several parallel streams of processing in a workspace, so it isn’t always apparent which transformers will be processed in which order.

Secondly, FME works by pushing features through the workspace on an individual basis, not as a group. For example, if there are three transformers in a workspace, the first feature is read and then processed by each transformer in turn. Then the next feature is read and processed by each transformer, and so on.

This makes for a log file that is harder to understand, because you don’t see one specific entry for each Reader or transformer in turn. Nor do you see a message for each feature. Instead, a cumulative time is calculated and output at regular time-based intervals.

**Translation Summary**

The final part of a log file includes a report of the number of features read and written but, more important from a performance point of view, it includes a brief report of the time taken by the translation and the amount of memory used:

Peak memory usage is an important statistic, as it is this number we’ll want to reduce in order to improve FME performance.

**Configuring the Log Window**

There are a number of options you can use to adjust the log file and what is displayed.

To do this, first Choose Tools > FME Options from the menubar.

Then choose the Translation set of options.

To assess times logged in the log window, you first need to turn them on! In the options menu, ensure that ‘Log timestamp information’ is turned on.

**NB:** *The log file always contains timestamps, regardless of this setting.
Now when a workspace is run, each message in the log gets stamped with the time and date it occurred.*

The Log debugging information option turns on a series of extra log messages that are usually hidden from the user. Not only will a lot of the underlying mapping file be exposed, there will also be a number of ERROR messages labelled BADNEWS.

These messages can help during debugging, but it’s very unlikely you’ll want to keep them turned on in general FME use. For instance, many of the BADNEWS messages are simple “errors” like an end-of-file message that FME has trapped and kept to itself. Unless you are looking for more information on an existing problem, these messages are likely to cause more confusion than clarity. Turn them off and de-clutter your log file.

A final set of options allow the user to turn on or off each type of message in the log window. It can be particularly useful to turn off INFORM and STAT messages in order to make it easier to spot ERRORs and WARNs; however it does appear strange at first to run a translation and not see the usual stream of information!

**Logs and Performance Indicators**

Let’s look at a few of the specific performance indicators we can identify in a log file and how we can improve upon them.

**Log Timings**

One interesting thing is that the cumulative time reported by a translation is the amount of time the FME process was actually translating or transforming data. It doesn’t include the amount of time spent waiting for other processes to do their work.

For example, take this section of  log timings:

2014-07-10 14:43:06| 8.5| 0.0|
2014-07-10 14:43:13| 8.8| 0.3|
2014-07-10 14:46:29| 18.0| 9.1|
2014-07-10 14:49:29| 25.8| 7.9|

The difference between the start absolute time (14:43) and the finish absolute time (14:49) is over six minutes. However, FME is only reporting 25.8 seconds of processing time!

The “lost” time is down to external processes that FME was waiting on.

For example, when a query is issued to a database, the time taken to respond with the results is not included in the FME processing time. The more a query is not well-formed or a database is not well-structured, the longer this time difference will be.

Similarly, the amount of time taken to read/write data from/to a disk is not included in this number.

Look at the section on Database Efficiency for more information on performance tuning FME for databases.

**Default Paths**

One of the most important paths to examine is the one for temporary folder. When memory resources become low and FME starts to cache to disk, the temporary folder is where it will write data to:

Firstly it’s important to ensure this folder does have enough temporary disk space and secondly it’s useful if the disk being written to is both fast and unused by any other process. It will not, for example, help performance to share the temporary disk with the operating system.

**Resource Manager**

One key message to look out for is this: ResourceManager: Optimizing Memory Usage. Please wait...

This means that the memory management limits mentioned in the configuration part of the log have been reached, and that FME is having to work around the issue.

If you see this message frequently, then it’s time to either redesign your translation or switch to a 64-bit setup.

**Written Features**

Maybe not quite performance-related, but one of the most misinterpreted statistics in an FME log is the number of features written.

What this really means is “the number of features sent to the Writer”. It doesn’t always mean the same number of features actually gets written to the output dataset, or that the output dataset will contain only that number of features.

For example, here 80 features are reported as sent to an (Esri Shape) Writer:

However, a warning earlier in the log tells us:

So in reality, the Writer rejected all of these features, in this case because their geometry was invalid. The Writer was set up to write line features, yet these are polygons.

Similarly, a format may have geometry limitations that cause the output dataset to be slightly different to the numbers logged.

For example, MicroStation DGN format has a limit on vertex numbers for each element (feature). If the MicroStation Writer receives a feature with too many vertices it will split that feature into multiple MicroStation features (elements in MicroStation speak) as many as necessary to avoid going over the vertex limit.

Thus, the number of features that actually appear in the dataset can be different to the number of features logged as being sent to the Writer.

Here we have a prototype workspace that processes a dataset of cell phone signals. The dataset contains a series of recordings that show how strong the cell signal is at different locations.

The idea is to filter out locations that receive a really poor signal, tag them with the neighborhood they belong to – to show which neighborhoods have poor coverage – and write the rest of the data out as a series of attribute-less data points.

However, the workspace runs perhaps a little slower than it could, which is bad news when this is just the prototype and we wish to eventually run it on the entire country’s cell data. First of all let’s check the workspace and deconstruct its log to find out what is happening.

**1)** Start Workbench

Open the workspace C:\FMEData2015\Workspaces\DesktopAdvanced\Exercise2a-Begin.fmw.

Notice there are two key feature types: one for the cell signals in CSV format, the other for the Neighborhood boundaries in KML format. They each have their own set of attributes:

There are also three transformers – two to attach the neighborhood and then filter the data – then two Writers, to write the data out to a final dataset. One has a few attributes, the other none.

The third transformer is a Logger that is recording features to the log.

Don’t run the workspace yet – we don’t know how long it might take!!!