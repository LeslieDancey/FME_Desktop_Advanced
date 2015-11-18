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