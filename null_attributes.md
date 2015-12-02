# Null Attributes

Null attributes are a relatively new, but very important, part of FME’s attribute handling.

**What is a Null Value?**

In general, a null attribute value is the equivalent of nothing. However, it’s important to be precise in our terminology when we talk about “null”. In reality there are many ways to represent nothing:

- An attribute is null
- An attribute exists but is empty
- An attribute doesn’t exist (i.e. is missing)
- An attribute is NaN (Not a Number)
- A numeric attribute has a value of zero

In fact, Safe Software’s developers have identified fifteen (15) different ways for “nothing” to be represented in spatial and tabular data.

So when we talk about null in FME, it has a particular meaning. For us, a null is an actual value that is deliberately set to signify that the information does not exist. It tells us that the lack of information is not a mistake – as a missing or empty value might.

How does FME Represent Null Values?
FME’s internal engine has its own state to represent null. However, when presented to the user, a null value is usually represented as <null>.

For example, this feature in the Logger has <null> for a number of attributes:

Similarly, the FME Data Inspector will depict nulls as <null>:

It can also differentiate between states by displaying <missing> or <empty> as well.

**Recognizing Null Values**

When FME reads data, if the source attributes contain nulls – and the Reader format has been updated to support them – then FME will emit that attribute with a null value.

To check for incoming nulls the Tester transformer has a specific operator to test for null, empty, and missing values:

Because the Tester interface is incorporated into many facets of FME (such as the TestFilter transformer) you can test for nulls wherever you find that interface.

Other transformers, such as the Matcher, also allow testing for nulls. In the case of the Matcher there is even a parameter that can be used to decide whether null, empty, and missing values should be treated equally, or as their own unique representation:

**Setting a Null Value**

The usual way to set an attribute value is with the AttributeCreator, and this has an option in its drop-down menu to set a value to null:

When you set an attribute to null, and send it to a Writer, then what happens depends upon the data format.

If the format supports nulls – and the Writer has been updated to support them too – then the destination dataset will contain null attribute values.

If the format doesn’t support nulls, then FME will automatically convert the data to the closest representation that is supported.

**Bulk Null Updates**

The way to handle bulk updates of attributes is with the NullAttributeMapper transformer.

The NullAttributeMapper transformer allows the author to check values for any or all attributes on a feature, and convert them in bulk to or from null.

For example, here the author is checking for all attributes that are either missing or empty, and converting them to nulls:

Here the author is checking a specific attribute for existing null values. If the value is set to null then it gets replaced with a zero. Presumably this must be a numeric field. If it was a text field perhaps instead the author would set it to an empty string:

<table style="border-spacing: 0px">
<tr>
<td style="vertical-align:middle;background-color:darkorange;border: 2px solid darkorange">
<i class="fa fa-quote-left fa-lg fa-pull-left fa-fw" style="color:white;padding-right: 12px;vertical-align:text-top"></i>
<span style="color:white;font-size:x-large;font-weight: bold;font-family:serif">Professor Lynn Guistic says…</span>
</td>
</tr>

<tr>
<td style="border: 1px solid darkorange">
<span style="font-family:serif; font-style:italic; font-size:larger">
“It’s good to be aware of nulls and test workspaces when updating from
FME versions prior to FME2014. Some formats and transformers may now
be producing null values where before they would have been either empty
or missing.”
</span>
</td>
</tr>
</table>