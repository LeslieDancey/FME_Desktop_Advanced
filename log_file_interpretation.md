# Log File Interpretation


If you can’t understand what FME is doing then there isn’t much chance you’ll be able to improve upon it.

The FME log file is your best friend for assessing performance. It tells you how long a translation took, where the time went, and how well FME was able to use the available system resources.

**Deconstructing a Log File**

The first thing to notice is that the log is made up of a number of messages, each of which consists of a number of fields:
- Absolute Date [Optional]
- Absolute Time [Optional]
- Cumulative Time (for translation)
- Elapsed Time (for this message)
- Message Type
- Message

We’ll look at the time fields later. The Message Type field will be one of the following:
- ERROR: An error in the translation that usually requires FME to terminate processing.
- WARN: A warning that signifies a problem that is not sufficient to terminate processing.
- INFORM: An information message relating a non-error item.
- STAT: A message on translation statistics such as the number of features processed.

The overall structure of an FME log is basically four different sections.

- Command-line statement
- Configuration and setup information
- The translation and transformation itself
- A summary of the translation

**Command-Line Statement**

At the very top of a log file appears the command-line statement. This is the command that FME Workbench is using to run the translation.