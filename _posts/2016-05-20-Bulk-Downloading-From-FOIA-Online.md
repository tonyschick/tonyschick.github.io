---
layout: post
title:  "Bulk downloading from FOIA Online"
date:   2016-05-20 23:43:00
categories: foia scraping
---

On the environment beat at [EarthFix](http://www.opb.org/news/topic/environment/), we file a decent number of Freedom of Information Act requests with the U.S. Environmental Protection Agency (EPA) and the National Oceanic and Atmospheric Administration (NOAA).

Both of those agencies rely on [FOIA Online](https://foiaonline.regulations.gov/foia/action/public/home), a site launched a few years ago that provides a web interface for filing and tracking FOIAs. Filing and tracking requests through the site is easy enough. But when a request comes back. actually downloading the records we requested is a serious pain. Downloads are limited to 20mb, and the site only displays 100 documents at a time. If a request comes back with hundreds or thousands of documents, and any of them are in the 1mb or over range, we essentially have to download them one at time. That's incredibly tedious. None of us really have time for it. It's actually slowed or stopped us in full diving into the records we've gotten back.    

Thus the need for the [FOIA Online bulk downloader](https://github.com/tonyschick/foia-online).

It's a simple, ugly yet effective script I wrote to download the files from a FOIA Online entry.

Run it from the command line, give it the url slug for your request, and go do something else. When it's done, you'll have a folder full of PDFs and a CSV that logged everything it downloaded.

I've tried it on a few of our past big requests, and it's worked well.

If you try and and spot any problems, let me know.
