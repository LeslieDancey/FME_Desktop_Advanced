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

**Improving Transformation Performance**

In most cases, slow, memory-consuming translations are caused by group-based transformers.

Remember that in feature-based transformation a transformer performs an operation on a feature-by-feature basis where a single feature at a time is processed. But in a group-based transformation a transformer performs an operation on a group or collection of features.

It is this grouping of data that causes performance degradation. Group-based transformers must store the group of features together (cached either to memory or disk) to be processed, whereas feature-based transformers do not need to do so.

<table style="border-spacing: 0px">
<tr>
<td style="vertical-align:middle;background-color:darkorange;border: 2px solid darkorange">
<i class="fa fa-quote-left fa-lg fa-pull-left fa-fw" style="color:white;padding-right: 12px;vertical-align:text-top"></i>
<span style="color:white;font-size:x-large;font-weight: bold;font-family:serif">Jake Speedie says….</span>
</td>
</tr>

<tr>
<td style="border: 1px solid darkorange">
<span style="font-family:serif; font-style:italic; font-size:larger">
“You’ll get better performance when you put the least amount of data
into a group-based transformer as possible.
For example, put feature-based filter transformers BEFORE the group-based process,
not after it (see following exercise)”
</span>
</td>
</tr>
</table>

**Turning Group-based Transformers into Feature-based Transformers**

Obviously, when a group-based transformer is needed, then it must be used. However, most group-based transformers have a parameter that, in effect, turns them into feature-based.

The usual parameter is called "Input is Ordered by Group" and appears near the Group By parameter in most transformer dialogs.

The condition for applying this is that the groups of features are pre-sorted into their groups.
When this is the case, and I can set this parameter to Yes, then FME is able to process the data more efficiently.

<table style="border-spacing: 0px">
<tr>
<td style="vertical-align:middle;background-color:darkorange;border: 2px solid darkorange">
<i class="fa fa-quote-left fa-lg fa-pull-left fa-fw" style="color:white;padding-right: 12px;vertical-align:text-top"></i>
<span style="color:white;font-size:x-large;font-weight: bold;font-family:serif">Jake Speedie says...</span>
</td>
</tr>

<tr>
<td style="border: 1px solid darkorange">
<span style="font-family:serif; font-style:italic; font-size:larger">
Let's think back to the airport departure gate boarding passengers. Most
airlines first call passengers with a physical disability, then passengers
with children, business-class passengers , and finally economy
passengers (starting with passengers at the front).
That's because it's easier to board passengers when they are sorted into similar groups,
and the same applies to FME. When passengers (or spatial features) arrive in a random
order it's not as simple to handle them.
</span>
</td>
</tr>
</table>

Besides the "Input is Ordered by Group" parameter, some transformers have their own, unique, parameters for performance improvements.

For example, the NeighborFinder expects two sets of data: Bases and Candidates. By default FME caches all incoming Bases and Candidates because it needs to be sure it has ALL of the candidates before it can process any bases.

But, if it knows the candidate features will arrive first (i.e. the first Base feature signifies the end of the Candidates) then it doesn’t need to cache Base features. It can process them immediately because it knows there are no more candidates that it could match against.

Look at this log file for a workspace that uses a NeighborFinder. By default it looks like this:

*Translation was SUCCESSFUL with 0 warning(s) (13597 feature(s) output)*

*FME Session Duration: 29.6 seconds. (CPU: 27.7s user, 1.5s system)*

*END - ProcessID: 28540, peak process memory usage: 231756 kb*

With Candidates First turned on it looks like this:

*Translation was SUCCESSFUL with 0 warning(s) (13597 feature(s) output)*

*FME Session Duration: 28.4 seconds. (CPU: 27.4s user, 0.8s system)*

*END - ProcessID: 26429, peak process memory usage: 178412 kb*

It’s about 5% faster than before, but more importantly it’s used nearly 25% less memory!

But how do we ensure the Candidate features arrive first? Well, like Writers you can change the order of Readers in the Navigator, so that the Reader at the top of the list is read first.

It doesn’t improve performance per se, but it does let you apply performance-improving parameters like this.

**Transformer Selection**

If you’ve used FME for any length of time, you’ll know that it’s possible to do almost any task in several different ways.

For example, you could check for matching features in two different datasets using either the Matcher transformer, or the ChangeDetector, or even the FeatureMerger!

Another example would be isolating all road features that pass through a park.

One could use either the Clipper, like so:

Or the LineOnAreaOverlayer, with a test for _overlaps => 1, like so:

The performance for the LineOnAreaOverlayer would be this:

While the Clipper (in Multiple Clippers mode) would be this:

And in Clippers First mode would be this:

So the result is the same, but the performance vastly different.

Obviously in the above example the Clipper is the fastest (and be sure to note how the Clippers First mode has reduced memory use by nearly 90%).

But each transformer has different functionality, and if you wanted to output park features with a list of roads or a count of the roads passing through the park, then the LineOnAreaOverlayer would be the transformer of choice, because it has a specific list parameter.

Basically, each transformer works in a different way, has subtle variances in functionality, and
will have different performance for any given task. Therefore a translation will benefit in
performance if the author is careful in their choice of transformers, and maybe carries out
some testing first.

**Attributes and Transformation**

As mentioned (in Reader Performance) reducing data helps performance because it saves FME
from either holding it in memory or caching it to a disk.

However, this isn’t just helped by reducing the number of features; it is also helped by reducing the size of each individual feature.

One aspect of this is attributes. Carrying attributes through a translation impacts performance, so if the attributes are not required in the output, it’s best to remove them as early as possible in the translation.

For example, the incoming schema looks like this:

But the outgoing schema looks like this:

Since so many of the source attributes are not required in the output, it makes sense to remove them from the translation, and as early as possible by using an AttributeRemover (or Keeper) directly after the source feature type:

One specific type of attribute to beware of is a List. A List is an attribute that can have multiple values. Because of this it can be a big drain on resources.

For example, use a Joiner to join a feature to 1000 records and the list for that feature will have 1,000 sets of records. This is bad enough, but if the list is exploded and all of the original attributes kept, then there will be 1,000 features each with 1,000 sets of attributes!

Another particular problem is carrying around spatial data as attributes. Spatial database formats - for example Oracle or GeoMedia - usually store geometry within a field in the database; for example GEOM. When FME reads the data it converts the GEOM field into FMEstyle geometry and drops the field from the data.

However, if you read a geometry table with a non-geometry Reader, the translation could end up with the geometry stored as an FME attribute. A similar thing could happen when a workspace reads only one geometry column of a multiple geometry table.

Geometry will create very large and complex attributes, which take up a great deal of resources. If you don’t need them, then it’s worth removing them.

Basically, you should only carry through the translation any geometry and attributes you need for the output of your workspace. If the data is not required, then it can and should be removed as early in the workspace as possible.

**Geometry and Transformation**

Like attributes, geometry can be removed from a feature using the GeometryRemover transformer.

Many FME users create translations that handle tabular – non-spatial – data. If you are reading a spatial dataset, then writing it to a tabular format, be sure to remove the geometry early in the workspace, just as you would an attribute.

Additionally, you can reduce the size of individual features by removing vertices. The Generalizer transformer will help you to do so and has very many parameters to control the results.

**General Optimizations**

Here are a few general suggestions that can be used to improve the performance of a workspace. Some of these come straight from our developers.

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
“It’s said that the race driver Michael Schumacher would tilt his head
slightly when racing, to allow more air into the engine intake.
If, like him, you measure performance down to the millisecond, then these tips are for
you!”
</span>
</td>
</tr>
</table>