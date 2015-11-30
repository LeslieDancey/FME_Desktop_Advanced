# Custom Transformer Versioning

FME includes functionality so that any single custom transformer can exist in a number of versions.

**Why use Versioning?**

Versioning means a single custom transformer can exist in any number of versions.

One advantage of versioning a custom transformer is that you have a record of previous versions and therefore can revert to a previous one should the need arise.

However, a more important advantage relates to FME releases and new functionality.

For example, a custom transformer shared by many users could be updated to use new behaviour in FME 2015. If that custom transformer is versioned then the previous version remains available to users who have yet to update to 2015, while users who have updated to FME2015 can update their custom transformer to match.

**Creating a Versioned Custom Transformer**

Versioning can occur whenever you edit a linked custom transformer and then attempt to save it. In that situation a dialog will open to ask what you wish to do: