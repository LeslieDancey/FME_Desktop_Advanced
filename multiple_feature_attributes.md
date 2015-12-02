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