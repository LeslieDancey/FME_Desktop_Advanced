# Parallel Processing

Parallel Processing is a way to improve performance on high-end machines.

**What is Parallel Processing?**

Each FME translation is usually a single process on your computer. Parallel processing is when you decide to transform your data as several simultaneous processes. The fact that they run simultaneously means the whole translation will run several times quicker than it used to.

The idea is to make use of multiple cores on a computer. There are four levels of parallel processing, and each maps to the number of cores in this way:

So, for example, on a quad core machine, minimal parallelism will result in two simultaneous FME processes. Extreme parallelism would result in eight.
There is also a hard cap for each license level:

So, if you have a Base Edition license you are never going to get more than four processes at one time, regardless of machine type and the parallelism parameter.

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
“Parallel Processing is very effective when you are offloading a task
elsewhere – for example calling a Server with the HTTPFetcher – as each
process is a tiny impact on the FME system resources.
However, be aware, each parallel process involves starting and stopping an FME engine,
and this takes time. So, don’t parallelize your processes when the task already takes
less than the time to stop/start FME!”
</span>
</td>
</tr>
</table>