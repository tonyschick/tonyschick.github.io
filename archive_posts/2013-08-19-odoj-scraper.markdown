---
layout: post
title:  "Scraping data out of the Oregon consumer complaints database"
date:   2013-09-06 12:19:00
categories: jekyll update
---

The Oregon Department of Justice keeps an online database of consumer complaints that is updated regularly. It's a fantastic tool, but it's primarily helpful if you already know what you're looking for. You can enter search terms for companies or search by date and get descriptions of the nature of the complaint and how the department handled it.

It's great public information, but it's not in the easiest format for really understanding the data. You can only view one record at a time, and you can't ask the online database which company has the most requests, or whether there are more requests happening than there used to be, or if one company got a slew of complaints all relating to a similar practice or incident. For that, you'd want tabular data, a spreadsheet -- columns and rows.

Enter web scraping. Using a programming language, you can write a script to tell your computer how to go fetch the records out of that online database and spit it back to you as a spreadsheet. What a wonderful world.

In my case, I used the Python programming language, which I've been working with for the past year. Using Python, I could automatically check to see how many records are in the database and retrieve them one by one -- this would take weeks of mind-numbing labor. The script took me a couple of hours to write and maybe another hour to clean out all the bugs (i.e. stuff I did wrong). It would take an expert programmer a lot less time. The scraper ran for about 42 hours while I was off doing whatever I wanted. And when it was done, [I had 64,146 records in a beatiful CSV file, ready to be worked with.](https://github.com/tonyschick/odoj).



<div style="float: left; width: 38.5%; margin: 1%;">
Before:
<img style="width: 100%" src="/imgs/odoj.png" />
</div>

<div style="float: left; width: 57.5%; margin: 1%;">
After:<img  style="width: 100%" src="/imgs/complaints.png" />
</div>

Web scraping, to me, represents one example of how coding can make you a better journalist. Much is made now of news applications and data visualizations, and for good reason, but I think the emphasis on knowing how to write code for those purposes distracts from how it can make journalists better at the jobs they already do every day. Programming can automate tasks that take up reporters' time and it can also do things that reporters could never do on their own. The ability to write a computer program doesn't just mean cool new web tools. It means you're a more dangerous reporter.

In my opinion, nobody puts this better than Ben Welsh of the Los Angeles Times Data Desk, when he talks about what he calls human-assisted reporting. [View his impassioned "lightning talk" at the 2013 NICAR Conference here](http://ire.org/conferences/nicar-2013/lightning/). Allow me to paraphrase and bastardize: Right now we treat computers like guns when we're going after a story. The story is out there, I'm going to find it, and I'm going to target it with my gun. But as journalists we should view "computer-assisted reporting" like the little spider robots in minority report -- we should write programs that constantly scour the city and deliver us stories.

We should also be standardizing all of our data. This doesn't just apply to people who work with Excel or statistics. It applies to anyone whose got a mess of a MyDocuments folder with 18 versions of the same file that's been slightly tweaked over and over again.

So how exactly does my lowly little scraper work? Well, you can check it out -- and access the resulting file -- here: [https://github.com/tonyschick/odoj](https://github.com/tonyschick/odoj)

I've included instructions on how to run it. If you want to run it and have trouble, [email me](/about/)	.
