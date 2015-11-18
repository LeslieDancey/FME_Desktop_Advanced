# Even More User Parameters

User parameters are very flexible and can be used in a variety of ways and scenarios

**Shared Parameters**

When a user parameter is used – either by an attribute or by being linked to an FME parameter – there’s no reason why it should only be used once. The value obtained from a user parameter can be used as many times as is required.

In this scenario it can be described as a shared parameter.

For example, here the tolerance in a Snapper transformer is being set by a user parameter called TOLERANCE. The value of that same parameter is being fetched into an attribute so it can be recorded in the output dataset:

Similarly, if there are two (or more) Snapper transformers in the workspace, they all might use the same user parameter for tolerance.

The advantage in this is that the same value can be used without the user having to enter it multiple times.

**Published and Private User Parameters**

When a user parameter is created, one of the options is a checkbox labelled “Published”:

The purpose of this option is to expose or hide the parameter from the end user. If the Published box is checked, then the user will be prompted to enter a value. If the box is unchecked then they will not.

Such a parameter is then listed as Private:

Private Parameters have two uses. Firstly, they are a way for the workspace author to share a value without having it exposed to the user.

For example, if the Snapper transformers (in the previous screenshots) needed to get a common value – but that value is set by the author, not the user – then a private parameter can be used. It allows the author to set all Snapper tolerances to the same value, but without exposing that option to the end-user.

The other use of a private parameter is when a user parameter only provides partial input, and the true value has to be constructed. This is done as an Embedded Parameter.

<table style="border-spacing: 0px">
<tr>
<td style="vertical-align:middle;background-color:darkorange;border: 2px solid darkorange">
<i class="fa fa-quote-left fa-lg fa-pull-left fa-fw" style="color:white;padding-right: 12px;vertical-align:text-top"></i>
<span style="color:white;font-size:x-large;font-weight: bold;font-family:serif">Ms. Analyst says….</span>
</td>
</tr>

<tr>
<td style="border: 1px solid darkorange">
<span style="font-family:serif; font-style:italic; font-size:larger">
“The Optional checkbox tells FME whether this user parameter is
compulsory or optional. Turn off the checkbox – like the author should in
the above example – when the input is a required field.”
</span>
</td>
</tr>
</table>

**Embedded Parameters**

An embedded parameter is when the value of one user parameter is used inside another.
For example, here the user is allowed to enter a filename, but not the path the data is written to.

A published user parameter is created to accept a filename from the user. A private user parameter constructs the full name from that input [as C:\FMEData2015\Output\$(UserFileName)].

Finally, the private parameter is linked to the FME parameter for the destination dataset: