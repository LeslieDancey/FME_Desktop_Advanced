# Custom Transformers and Parallel Processing

Parallel Processing is a way to improve performance on high-end machines.

As noted in the Performance chapter, some FME transformers have the option to allow parallel processing. However, custom transformers have a special mechanism to do this. Whereas not all FME transformers allow parallel processing, you can apply this technique to ANY custom transformer that you like!

**Setting up Custom Transformer Parallel Processing**

Parallel processing for a custom transformer is set up in the Navigator window.
Each custom transformer has a set of transformer parameters that specifically relate to parallel processing. Here you can determine the level of parallel processing, and the attribute that is going to be used to define the processing groups:

By default, these are set to not carry out parallel processing. However, when the author sets a level of parallelism then the Parallel Process By parameter becomes active and a user parameter is automatically created:

<table style="border-spacing: 0px">
<tr>
<td style="vertical-align:middle;background-color:darkorange;border: 2px solid darkorange">
<i class="fa fa-quote-left fa-lg fa-pull-left fa-fw" style="color:white;padding-right: 12px;vertical-align:text-top"></i>
<span style="color:white;font-size:x-large;font-weight: bold;font-family:serif">First Officer Transformer says…</span>
</td>
</tr>

<tr>
<td style="border: 1px solid darkorange">
<span style="font-family:serif; font-style:italic; font-size:larger">
“Because of how parallel processing works in a custom transformer, you
can’t use an attribute for the Parallel Process By parameter. Instead you
have to make use of a user parameter that references an attribute.
In short, you can’t select an attribute in this dialog, only user parameters.”
</span>
</td>
</tr>
</table>