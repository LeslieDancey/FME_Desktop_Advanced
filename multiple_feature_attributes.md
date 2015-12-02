# Multiple Feature Attributes

Normally a feature in FME is self-contained. It might get processed as a group at some point, but other than that it doesn’t have any sort of relationship to other features in the workspace.

However, in some cases the ability for a feature to access the attributes of other features would be quite useful.

For example, take a tabular dataset of coordinates that are recorded as follows:

XY

+0.0 +3.0

+3.2 +0.0

-3.2 +0.0

+0.0 +3.4

+4.2 +0.0

In this case each row is not an absolute coordinate; instead it is an offset from the previous one. Therefore, to calculate the true coordinates, each feature would need to know the coordinates of the previous feature, so that it could apply the offset.

This sort of scenario is catered for by Multiple Feature Attributes in FME.

**Multiple Feature Functionality**

Multiple feature functionality is activated by checking the box labelled Prior/Subsequent Feature Attribute Retrieval in an AttributeCreator transformer:

This opens up a section of dialog in which the author can specify how many features preceding the current feature, or how many features that succeed it, should be made available.

There is also an option to specify what should happen if the attributes are missing from a prior/subsequent feature. There is the ability to use a fallback value (which might just be an empty string), to use the value of the closest feature that does contain the attribute, or to use an attribute value instead.

Using Multiple Feature Attributes

The simplest way to make use of the attributes retrieved from prior/subsequent features is through the text or arithmetic editors.

In the editors, the list of feature attributes will have an expandable section for prior and subsequent features: