# Module Review

This chapter looked at FME Performance and some of the techniques available to improve it

**What You Should Have Learned from this Module**

The following are key points to be learned from this session: 

**Theory**

- Performance is the measure of useful work done in a given time. Excess data and caching of data to disk are two factors that can impact performance greatly.
- 64-bit FME can make use of more system memory, but does not have the same format reach that 32-bit FME does
- Analyzing a log file helps to determine where performance improvements can be made.
- Improve reading performance by reducing the amount of data being read. Improve writing performance by ordering the FME Writers correctly. Improve transformation performance by removing excess attributes and properly managing group-based transformers.
- Make use of all Reader/Writer parameters to improve database performance.
- Employ parallel processing to make FME multi-threaded.
- Upload larger tasks to multiple engines on FME Server. 

**FME Skills**

- The ability to analyze and deconstruct an FME log file
- An understanding of potential methods for improving Reader, Writer, and transformer performance
- The ability to use database parameters to improve performance
- The ability to apply parallel processing in an FME workspace