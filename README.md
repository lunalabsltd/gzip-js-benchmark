What's that?
============

A very basic docker-compose stack containing JSON files in two folders served by an Apache. The configuration is set up so that files residing in www/gzip/ folder are served as gzip-encoded content (pre-compressed), while files in www/nogzip/ folder are served as is.

The index.html page contains a simple JS code that runs 1000 iterations fetching these files and reports and average time a request took to complete.

The purpose of this demo is to illustrate if gzip has any effect on performance.

Does it?
========

Yes and no. When running tests on local environment (to eliminate network transmission speed jitter), the effect is really umeasurable - which is expected as per benchmarks found on the Internet (i.e. https://tukaani.org/lzma/benchmarks.html)

Sample of results
--------------------------------------------------------
When running over loopback / wire connection (iPhone), the results we have observed were as follows:

| Device           | no gzip, ms | gzip, ms |
|------------------|-------------|----------|
| Macbook Pro 2014 | 6.01        | 6.06     |
| iPhone 7         | 11.63       | 11.79    |

When tests are carried out involving network (even local WiFi would be enough to manifest the effects), gzip variant turns out to be a clear winner, because sub-millisecond decompression delay still justifies 2-3x reduction in wire size:

| Device           | no gzip, ms | gzip, ms |
|------------------|-------------|----------|
| Macbook Pro 2014 | 28.56       | 13.74    |
| iPhone 7         | 29.49       | 17.73    |

Conclusion
==========

The performance of gzip encoding has little to no effect on runtime performance of both desktop and mobile devices, which is supported both by theory (gzip benchmarks) and practice (this suite being an example).