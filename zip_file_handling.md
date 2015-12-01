# Zip File Handling

Zip files are a convenient way to write output datasets that need to be handled as a single unit.

The Basic Desktop course covered how data can be read directly from a zip file. However, it is also possible to write data to a zip file.

Zip files are a convenient way to write output datasets that need to be handled as a single unit.

For example, a single Shape feature type consists of several files; shp, shx, dbf, prj, etc. A Shape dataset can consist of multiple feature types. So, in a scenario where the output data needs to be post-processed – uploaded to a web site, say – it’s more convenient to handle a single zip file than multiple data files.

**Zip File Writing**

The simplest way to create a zipped output is to simply change the file extension to .zip in the output dataset field:

A small icon in the dataset field indicates the zipped status:

When the workspace is run the log file reports the zip creation:

And the output is, indeed, a zipped dataset: