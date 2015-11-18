# Transformation Optimization

Now that you can interpret a log file, you can start to work on improving the performance of your data transformation.

**Assessing Transformation Performance**

As with Readers and Writers, you can’t make performance improvements unless you can accurately interpret a log file and measure a baseline performance for your translations.

If you want to be able to assess the time taken in transformation then the first thing to do is calculate the read time so that it can be ignored. So firstly disable everything in the workspace except the Readers and run the workspace. Take a note of the elapsed time.

Now re-enable the transformers, but leave the Writers disabled.

Don’t be tempted to add an Inspector or Logger transformer to the end to see what is happening to the output. This will only slow the translation down and give you a false measure.
And be sure to disable the actual Writer, and not just the feature types or connections to them.

The one Writer that is useful in this scenario is the Null format Writer.

This causes a Writer to be present, but it does nothing except to log features and then discard them.

The benefit is improved logging of feature counts, but without any data having to be written.

