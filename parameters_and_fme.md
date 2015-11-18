# Parameters and FME

Parameters control how FME operates, and can be set by either the workspace author or the end user.

**What are Parameters?**

Parameters, in basic terms, are controls that define how FME operates; for example, how a
Reader reads data, how a transformer transforms it, and how a Writer writes it.
Almost every component in FME has parameters; of one type or another.

**Types of Parameter**

When looking at the types of parameter, it’s helpful to consider the types of people who use FME and their role in the process.

Workspace Authors are the people who design and create a workspace. They use FME
Workbench and set parameters to control how the workspace runs.

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

Here, for example, are the FME Parameters for a text file Writer. They include options to overwrite or append to an existing text file, and the type of character encoding that should be
used.