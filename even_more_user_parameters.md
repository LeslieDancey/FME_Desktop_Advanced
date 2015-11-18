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

The RealFileName parameter is obviously kept private because the user doesn’t need to know about it, much less set a value for it.

In this example the private parameter was created using a text editor. All user parameter creation dialogs have the ability to open a text editor. This is where simple concatenation of other parameters with fixed values can take place:

**Scripted Parameters**

A scripted parameter is a special type of user parameter.

Scripted parameters go one step further than an embedded parameter.

Whereas an embedded parameter allows simple construction of a new value by concatenation, a scripted parameter allows a full Python or TCL script to be used to construct a value.

For example, here is the definition for a TCL scripted parameter that, again, concatenates a filename from the user with a set path from the author.

However, in this case, the script is used to test whether the workspace is being run on a Windows or Linux system, so it can set the output path accordingly:

Note that the script must include a return statement, to return a value to the parameter.

All Scripted Parameters are private by default, and can never be published, as it’s obviously absurd for a user to be entering Python code when a workspace runs!

<table style="border-spacing: 0px">
<tr>
<td style="vertical-align:middle;background-color:darkorange;border: 2px solid darkorange">
<i class="fa fa-quote-left fa-lg fa-pull-left fa-fw" style="color:white;padding-right: 12px;vertical-align:text-top"></i>
<span style="color:white;font-size:x-large;font-weight: bold;font-family:serif">Ms. Analyst says…</span>
</td>
</tr>

<tr>
<td style="border: 1px solid darkorange">
<span style="font-family:serif; font-style:italic; font-size:larger">
“Use the ‘print’ command (in Python) or ‘puts’ command (in TCL) to write
from the script to the FME log file.”
</span>
</td>
</tr>
</table>

**Attribute Name Parameter**

Sometimes an FME parameter is designed to accept either a fixed value or the value of an attribute. We call these parameters _OR_ATTR parameters, because they allow a value OR an attribute.

For example, this LabelPointReplacer allows the label to come from a fixed value, or an attribute: