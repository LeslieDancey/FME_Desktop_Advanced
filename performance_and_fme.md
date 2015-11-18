# Performance and FME

Performance means producing the results you need as efficiently as possible.

**What do we mean by Performance?**

According to Wikipedia, performance is a measure of the amount of useful work accomplished relative to the time and resources used.

In FME terms, good performance is the ability to process spatial and tabular data with the correct results (useful) as fast as possible (time) and using as few system resources – like memory – as possible.

**What Can Impair Performance?**

There are a number of factors – you might call them bottlenecks – that can cause FME to run slower than you might hope. Most of the content of this chapter covers how to overcome or relieve these factors.

In particular, some such factors are:
- Excessive Disk Operations

Physical disk drive throughput is relatively slow compared to other computing processes; therefore the more FME has to read and write to a physical disk drive, the more performance is impaired. The best performance comes from storing temporary data in memory, rather than on disk.

- Underuse of Resources

Performance can be impaired when an FME translation is not using all of the available system resources. For example, there are minimal licensing limits that prevent FME from using all of the CPU cores on a system, and more memory resources are available to 64- bit FME than 32-bit.

- Excessive Data Amounts

If performance is described as the amount of “useful” work, then nothing is going to impair performance more than unnecessary processing. The more excess information that gets read, and the further it is carried into the workspace, the less useful the work is and the more performance will suffer.