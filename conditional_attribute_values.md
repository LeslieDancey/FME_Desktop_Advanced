# Conditional Attribute Values

Conditional Attribute Values are a tool that can be used to replace many existing transformers of the same type.

**Transformer-Based Attribute Mapping**

The Basic FME Desktop training course includes a section on Conditional Filtering, and explains how to apply conditions to data in order to split or divide it into multiple streams.

In this example, the AttributeFilter is being used to divide data on the basis of a postal code attribute value:

Similarly, a Tester or TestFilter transformer can be used to divide data in various ways.

So filtering transformers divide data up into separate streams in the workspace. The question is: what happens when the scenario requires a new attribute to be created based upon the original attribute value?

Technically, the following works, but it is far from elegant:

There are just far too many AttributeCreator transformers. Imagine if there were 100 values to handle! The workspace would be enormous!

In that scenario, the solution would be to use a simple AttributeValueMapper transformer:

However… what if the original attribute required a more complex condition to carry out the mapping? In that scenario something even more advanced would be required: Conditional Attribute Values.

**What are Conditional Attribute Values?**

Conditional attribute values are when the author sets an attribute value, but conditional upon a number of tests that must be first applied to the data.

The option for conditional attributes is found in the drop-down dialog on most transformer parameters. In the AttributeCreator, it appears like so:

The Conditional Definition dialog looks like this: