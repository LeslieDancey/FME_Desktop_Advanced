# Transformation Optimization

Now that you can interpret a log file, you can start to work on improving the performance of your data transformation.

**Assessing Transformation Performance**

As with Readers and Writers, you can’t make performance improvements unless you can accurately interpret a log file and measure a baseline performance for your translations.

If you want to be able to assess the time taken in transformation then the first thing to do is calculate the read time so that it can be ignored. So firstly disable everything in the workspace except the Readers and run the workspace. Take a note of the elapsed time.

Now re-enable the transformers, but leave the Writers disabled.

Don’t be tempted to add an Inspector or Logger transformer to the end to see what is happening to the output. This will only slow the translation down and give you a false measure.
And be sure to disable the actual Writer, and not just the feature types or connections to them.

The one Writer that is useful in this scenario is the Null format Writer.

This causes a Writer to be present, but it does nothing except to log features and then discard them.

The benefit is improved logging of feature counts, but without any data having to be written.

Now I know it took 5.4 seconds to read the data, and the whole process took 28.2 seconds, so I can infer that the transformation part takes 22.8 seconds.

With the Reader and Writer figures as well, I now have a complete breakdown of how long each section of my workspace takes.

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
“In a larger workspace you could isolate different sections by disabling
different connections, and therefore determine the performance of
individual parts of the workspace.”
</span>
</td>
</tr>
</table>

However, the time taken to carry out a translation is only one aspect of performance. Another important aspect is the amount of memory used during processing. You can’t tell how much memory each individual transformer used, but you can see the maximum memory used during a translation by examining the very foot of the log file:

*INFORM| Translation was SUCCESSFUL with 0 warning(s) (13597 feature(s) output)*

*INFORM| FME Session Duration: 28.3 seconds. (CPU: 27.3s user, 0.6s system)*

*INFORM| END - ProcessID: 28336, peak process memory usage: 178388 kb*

For performance tuning, the idea is to reduce this number, as the more memory used the more chance there is of laborious disk caching taking place.