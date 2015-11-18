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