# Parameters and FME

Parameters control how FME operates, and can be set by either the workspace author or the end user.

**What are Parameters?**

Parameters, in basic terms, are controls that define how FME operates; for example, how a Reader reads data, how a transformer transforms it, and how a Writer writes it.
Almost every component in FME has parameters; of one type or another.

**Types of Parameter**

When looking at the types of parameter, it’s helpful to consider the types of people who use FME and their role in the process.

Workspace Authors are the people who design and create a workspace. They use FME Workbench and set parameters to control how the workspace runs.

Workspace Users are the people who make use of a workspace, without necessarily having created it first. The user might have very little knowledge of FME, and may never have used

FME Workbench, but they still may need to set parameters to control how the workspace runs.
In light of these two roles, we can say there are two different types of parameter.

**FME Parameters**

FME parameters are those built into FME. They directly control a translation and can be found in various places, such as transformer dialogs or feature type dialogs. However, for the most part you will find all FME Parameters in the Navigator Window of FME.

Parameters:
- Overwrite Existing File: Yes
- Line Termination: System
- Write Last Line Terminator: Yes
- Character Encoding: SYSTEM
- Write UTF Byte Order Mark: Yes

Here, for example, are the FME Parameters for a text file Writer. They include options to overwrite or append to an existing text file, and the type of character encoding that should be used.

These are parameters the workspace author will use. The user is not expected to set these, because the user may have no experience of Workbench and not know where to find the parameter or how to set it.

For example, the author might decide that the Byte Order Mark should not be written in this output.

They double-click the parameter to open a dialog in which they can change the parameter value.

**User Parameters**

User Parameters are those that are created by an FME author for use by an FME user. In other words, they are a way for the end-user of the workspace to provide their input to a workspace.

User parameters appear in a special section of the Navigator window, labelled User Parameters. Here, for example, two user parameters are defined.

*User Parameters:
 
  Published Parameters
  - [SourceDataset_FILEGDB] Source Geodatabase: C:\FMEData2014\Data\Addresses\Addresses.gdb
  - [DestDataset_TEXTLINE] Destination Text File: C:\FMEData2014\Output\GarbageSchedule.html
  
  
Each user parameter allows the end-user of a workspace to enter information. This may be through a simple dialog (in Workbench or the FME Quick Translator) or it might be through a web page on FME Server.

<table style="border-spacing: 0px">
<tr>
<td style="vertical-align:middle;background-color:darkorange;border: 2px solid darkorange">
<i class="fa fa-quote-left fa-lg fa-pull-left fa-fw" style="color:white;padding-right: 12px;vertical-align:text-top"></i>
<span style="color:white;font-size:x-large;font-weight: bold;font-family:serif">person X says...</span>
</td>
</tr>

<tr>
<td style="border: 1px solid darkorange">
<span style="font-family:serif; font-style:italic; font-size:larger">
Ms. Analyst says…
“We used to use the term Published Parameters. It sort of still applies – you
can see it used in the screenshot above – but there’s some confusion, as
we’ll see. It’s better to use the term User Parameters.”
</span>
</td>
</tr>
</table>
