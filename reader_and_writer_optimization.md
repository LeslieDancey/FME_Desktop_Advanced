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