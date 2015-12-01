# The Generic Reader/Writer

The Generic Reader and Writer allow FME workspaces to be freed from format restrictions.

**Generic Formats**

FME’s generic tools are a Reader and Writer that are not tied to a particular format. The Generic Reader is capable of reading almost any format of data, and the Generic Writer is capable of writing almost any format of data.

In that way, a single workspace can be used to process different data formats without being specifically set up for that format.

**The Generic Reader**

Whereas all other Readers are tied to a particular format, the Generic Reader is capable of handling almost any format.

A Generic Reader is simply added the same way that any other Reader is used; by specifying the format in the new Reader dialog:

A parameter allows the format of the data being read to be specified, or it can be left up to FME to ascertain the format from the data extension of the source file.

Now at run time, the source dataset can be set to GML:

Or MapInfo TAB:

Or any other format of data you care to read (provided the data has the same schema). This makes for a very flexible workspace.

Generic Reader Feature Types

However, the Generic Reader is not immune from the Unexpected Input Remover. Remember, this is the functionality that filters incoming data against the list of feature types (layers) that are defined in the workspace. If the incoming data is stored on a layer that is not defined in the workspace, then it will be removed.

For this reason, you’ll want to ensure that all potential layers are defined as feature types in the workspace; or that you have a Merge Feature Type set in the Feature Type Properties dialog: