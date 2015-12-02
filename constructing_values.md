# Constructing Values

Constructing Values goes one step further than setting an attribute with a simple, fixed value.

FME has various functions that allow the workspace author to create a simple, fixed value for an attribute.

For example, here an author is using the AttributeCreator transformer to set the value of an existing attribute and to create a new attribute with a fixed value:

However, in many cases the workspace requires a value to be constructed out of a number of existing values, or perhaps an arithmetic calculation, and FME is capable of doing that as well.

There are, basically, two methods to constructing attribute values: Transformer Construction and Integrated Construction.

**Transformer Construction**

Transformer construction is a basic method of constructing attribute values. The author sets simple values in a transformer, but uses two or more transformers in a series in order to build a more complex value.

For example, here the workspace author needs to create a label in their spatial data.