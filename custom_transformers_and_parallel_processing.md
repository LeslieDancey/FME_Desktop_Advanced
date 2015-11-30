# Custom Transformers and Parallel Processing

Parallel Processing is a way to improve performance on high-end machines.

As noted in the Performance chapter, some FME transformers have the option to allow parallel processing. However, custom transformers have a special mechanism to do this. Whereas not all FME transformers allow parallel processing, you can apply this technique to ANY custom transformer that you like!

**Setting up Custom Transformer Parallel Processing**

Parallel processing for a custom transformer is set up in the Navigator window.
Each custom transformer has a set of transformer parameters that specifically relate to parallel processing. Here you can determine the level of parallel processing, and the attribute that is going to be used to define the processing groups:

By default, these are set to not carry out parallel processing. However, when the author sets a level of parallelism then the Parallel Process By parameter becomes active and a user parameter is automatically created: