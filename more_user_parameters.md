# More User Parameters

There are many different types of user parameters and many different ways to make use of them.

**Types of User Parameters**

One of the key parameters when creating a user parameter is the parameter type. There are many different types, of which the more common ones are:

- Choice
- Choice with Alias
- Float
- Integer
- Text and Text (Multiline)

**Choice and Choice with Alias**

A choice parameter is when the user is presented with a fixed list of options and selects one of them. Here is a similar example to before. The user is being asked to enter their name. However, the names of all users are already known – presumably this is for a particular company’s staff – so a list of them is created:

That way, the user is prompted to select their name from a list. They don’t have to type it in manually.

A Choice with Alias parameter is the same as a Choice parameter in that the end-user gets to pick a value from a list. However, a lookup table maps the chosen entry to a value that gets provided to FME.

For example, this workspace takes incoming features and matches them to a database using an EmployeeID.

EmployeeID is provided by the end-user, but they can’t always remember their own ID number. So, the author creates a Choice with Alias user parameter.

The parameter is configured like so:

Notice that there are two fields in this configuration dialog; the display name and the actual value