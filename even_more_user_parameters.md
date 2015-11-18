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