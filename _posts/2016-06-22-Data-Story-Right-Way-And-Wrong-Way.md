---
layout: post
title:  "Workflow for a data story: The right way and the wrong way"
date:   2016-06-22 20:05:00
categories: data workflow
---

Last month I gave a guest presentation to a class learning data journalism techniques through Hack Oregon.

They were interested in workflow. I've become a bit obsessive about finding good workflows. So I showed them a couple of recent stories. One had a workflow I was proud of: One Python script, annotated, completely traceable and repeatable from start to finish. The other was a complete mess: Half a dozen Excel files, several different softwares used.

I don't work on a data team. This is not a rare case. I'm the only person on my team that uses data with any regularity and the only one who writes code. We don't have a data editor who scrutinizes my steps. Everything I do has to be exacting. I have to catch the mistakes, because no one else will.

An answer to that, learned through several NICARs, is to have a rock-solid and reproducible methodology.

In the ideal, everything is documented and reproducible. Every piece of the process -- every sort, calculation, renaming of columns or trim of trailing spaces. The code to achieve it is published and the reason for it is documented.

The closest I've come to this, so far, is in a [story from earlier this year](http://www.opb.org/news/article/backlog-grows-for-rangelands/) about lagging enforcement of environmental protections on public lands used for livestock grazing. All of the code used in the project was [published on GitHub](https://github.com/Oregon-Public-Broadcasting/rangeland). The Python code for cleaning and analysis was annotated in a Jupyter Notebook.

There were so many benefits to this process. It wasn't an easy analysis, but it was nice and tidy. It allowed me to explore the data quickly and with a trail of what I'd done. When finished, I shared the entire analysis with the Bureau of Land Management, the source of the data and the target of the story, and discovered the source discrepancies in the data I used and the data in their annual reports. After I published the story, I heard from a handful of scientists and other researchers who wanted to use the data in various ways.

I'd turned a corner in methodology. Until the next deadline came, and I hadn't.

The next significant story I produced was an investigation into [lackluster responses to air quality complaints](http://www.opb.org/news/series/portland-oregon-air-pollution-glass/neighbors-to-north-portland-polluter-say-deq-ignored-their-complaints/) at the Oregon Department of Environmental Quality (DEQ).

We wanted to compare air quality complaint responses in Oregon and nearby states, which is easier said than done. Washington, the natural state comparison for all things Oregon, has not one state clean air agency but seven different regional agencies in addition to the Washington Department of Ecology. Oregon has one of those regional air agencies, the rest is under the Oregon DEQ's authority.

Gathering data from 10 different agencies in the span of two weeks was a nightmare. Endless phone calls and emails as I negotiated for access and lower records fees.

Cleaning and analyzing the data was more painful. Each agency kept their data in a different format. Some agencies sent multiple Excel files of data. Some sent PDFs.

Our analysis was going to search for inspection and enforcement histories at facilities that were the subject of 10 or more complaints. That required serious name cleaning, as the data in almost all cases was entered by hand and one company could have been entered 10 different ways (for instance "Daimler Trucks North America", "Daemler Trucks", "Daimler", "Daimler Trucks NA" , "Daimler on Swan Island" or in a few cases "I'm pretty sure it's Daimler" or "Everyone thinks it's Daimler").

My original plan was to do the analysis in one annotated Python script, in accordance with my newfound enlightenment. I'd also just been to NICAR and learned about a new library called [dedupe](https://github.com/datamade/dedupe), which identifies duplicate entries. The stars were aligning.

As a test, I tried running dedupe on the first dataset I had. I tried implementing it like I learned but I messed something up. It didn't work, and I didn't know why.

Meanwhile, Portland's air quality was a hot story, news was breaking constantly. Every day I didn't deliver this story was costing us coverage elsewhere.

I panicked, and scrapped the idea of using a new tool.

Instead, I brought each file into [Open Refine](http://openrefine.org/) and later tallied complaints in Excel pivot tables. Open Refine is a great tool for name cleaning, and did let me trace every change I made to the original data. But this path meant I had 10 Open Refine projects going at once, and publishing a readable analysis the way I had for the grazing lands story just wasn't going to happen.

After I had the list of companies with 10 or more complaints, I sent them to each agency and asked for any inspections or enforcement actions in that same timespan, and whether they were triggered by complaints.

When I got those results, it meant a lot of by hand matching.

The two stories are quite different. I can't say one is stronger than the other.

By the end, I was just as confident in the analysis for the air quality complaints story as I was for the grazing lands story. But that's only because I stayed up till 3 a.m. several nights in a row before the story ran, re-doing the analysis and thoroughly checking each record for the companies in the analysis.

I wonder if I'd stuck with the original plan a little longer, if I'd trusted the process and suffered the headaches on the front end, maybe I could have saved myself from some of the stress and late nights at the computer.
