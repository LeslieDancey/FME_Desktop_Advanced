# Performance, FME Server, and FME Cloud


FME Server adds an extra dimension to FME performance.

In terms of performance, the prime reason for using FME Server is one of scalability, and the main consideration is the number of FME engines.

Increasing the number of engines supports a higher volume of jobs and the FME Server Core contains a Software Load Balancer (SLB) to distribute jobs to the FME engines in a balanced way.

In this scenario, FME Server is used not for its web-based abilities, but rather for its potential in processing large amounts of data in relatively less time.

**Using Server for Bulk Translations**

By default, utilizing multiple engines is only possible when you have multiple workspaces that can be run. When you have only a single workspace, and wish to process it more efficiently on FME Server, then you need to divide that workspace into multiple jobs.

For example, I have a very large set of vector data in a spatial database, and want to create a series of map tiles from it. Basically I need to clip the data to a map tile outline, rasterize it, and write it out to a raster format such as PNG: