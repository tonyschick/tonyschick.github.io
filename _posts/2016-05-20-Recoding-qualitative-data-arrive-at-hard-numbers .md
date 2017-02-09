---
layout: post
title:  "Recoding qualitative data to arrive at hard numbers"
date:   2017-02-08 23:43:00
categories: analysis spreadsheets
---

For a [recent story on Oregon’s handling of sensitive wildlife species](http://www.opb.org/news/article/wildlife-neglected-how-oregon-lost-track-of-sensitive-species-its-supposed-to-protect/), I sought to quantify how much the state knows about wildlife like reptiles, amphibians and small mammals that are not hunted or fished.

The state’s Department of Fish and Wildlife keeps a list of high-priority species, available in spreadsheet, and I’d heard from several sources that the state had done a poor job of keeping track of the ones on it. I wanted to know for which species the state knew how many exist, where they exist and whether the population was increasing or decreasing.

The data inside the spreadsheet was largely qualitative. Specifically, each species entry included one field called “data gaps”, which were essentially large text blocks with a narrative description of what the agency didn’t know about a species. Here’s an example:

“Assess distribution and abundance. Develop methods to survey this species in a variety of habitat types and features (logs, talus, etc.). Examine habitat associations in forests, including the effects of fires on this species. Assess sensitivity to herbicides and other chemical contaminants. Investigate dispersal capabilities, factors promoting movement, and home range size. Increase knowledge of reproductive habits, longevity, and over-wintering behavior.”

There was no way to analyze over a hundred of these in any meaningful way, so I began to recode them. I read through all of the entries to get a sense of what type of information they held. Once I had that, I began to make new categories based on the information I wanted and what was available. I wanted to know how many species had unknown populations, or where the effects of climate change, herbicides or other land uses were unknowns.

I made new fields: “abundance”, “distribution”, “trend”, “population makeup”, “habitat requirements”. I went through each entry again, and marked an 1 in each of those where the narrative mentioned them.

By the end, I had fields I could count, filter and sort. That taught me a lot about the state’s sensitive species and lead to a small but crucial line in the story: “Today, the state still lacks basic information such as geographic range, population status or habitat requirements for at least half the species on it.”
Recoding this data required a solid understanding of it. I talked with several people who worked with the data and created it. The Oregon Department of Fish and Wildlife’s data analyst was supportive of the effort, others at the agency were less so, and were concerned the data would be misinterpreted. Among their concerns were that the narrative fields were compiled with input from outside experts, and not meant for hard categories.

Given those concerns, I also spoke with some of the biologists who wrote the descriptions in the data gap field.  These conversations left me with a better understanding, and feeling comfortable enough to proceed with the data.
