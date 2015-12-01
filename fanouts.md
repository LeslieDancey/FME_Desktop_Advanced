# Fanouts

Fanouts are one of the most powerful pieces of functionality within FME, capable of producing impressive results with very little effort.

**What is a Fanout?**

Fanouts are a way for the workspace author to divide data up into groups of features, as the final step of a translation.

Because a fanout occurs as the data is being written, it does not cause multiple flows of data inside the workspace. Therefore this technique makes it easy to create groups with minimal impact on the workspace canvas.

Similarly to a group-by, the groups are defined by an attribute.

For example, here an author is “fanning-out” a set of data into multiple outputs depending on a feature’s elevation attribute:

A major benefit of a fanout is the high degree of flexibility – and freedom from fixed-layer schemas – in return for minimal effort.
There are two types of fanout: Feature Type Fanout and Dataset Fanout.

<table style="border-spacing: 0px">
<tr>
<td style="vertical-align:middle;background-color:darkorange;border: 2px solid darkorange">
<i class="fa fa-quote-left fa-lg fa-pull-left fa-fw" style="color:white;padding-right: 12px;vertical-align:text-top"></i>
<span style="color:white;font-size:x-large;font-weight: bold;font-family:serif">Sister Intuitive says…</span>
</td>
</tr>

<tr>
<td style="border: 1px solid darkorange">
<span style="font-family:serif; font-style:italic; font-size:larger">
“If this technique sounds familiar, that may be because it carries out a
similar function – albeit in reverse – to the “Merge Feature Type”
parameter.”
</span>
</td>
</tr>
</table>

**Feature Type Fanout**

A Feature Type Fanout delivers data to multiple feature types (layers) within a single dataset.

Taking the elevation example, here the output is a different feature type for each elevation value: