# Fanouts

Fanouts are one of the most powerful pieces of functionality within FME, capable of producing impressive results with very little effort.

**What is a Fanout?**

Fanouts are a way for the workspace author to divide data up into groups of features, as the final step of a translation.

Because a fanout occurs as the data is being written, it does not cause multiple flows of data inside the workspace. Therefore this technique makes it easy to create groups with minimal impact on the workspace canvas.

Similarly to a group-by, the groups are defined by an attribute.

For example, here an author is “fanning-out” a set of data into multiple outputs depending on a feature’s elevation attribute: