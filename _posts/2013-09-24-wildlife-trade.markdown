---
layout: post
title:  "Visualizing wildlife trade data"
date:   2013-09-24 12:19:00
categories: jekyll update
---

I’ve been wanting to use wildlife trade data for a long time. Wildlife trafficking fascinates me. I’ve also been looking for a data viz project, because after seeing it in action and reading/hearing about how great the javascript library is for working with data, I’ve been eager to build something of my own with D3js.

Putting the two together was pretty fun. 

What I originally (and still) wanted to do, was access the full database and build a web application that allowed users to search trades over time as well as view visualizations of trade trends, trades between countries, and traffic for each species. But I can’t do that yet, because I don’t have full access to the database (more on this below). Right now, the visualization shows live wildlife trade for 2011, the latest year available. Coming next is the addition of non-live trade such as animal parts, which is a little trickier because some of them are measured in units, some in milligrams, some in other metrics, etc. So once I clean that up and figure out how to aggregate the data given the various units of measurement, you’ll be able to see that here as well.

I then opted to create an initial visualization and build on it when I could. Looking through the D3 examples of different visualizations, I realized the chord diagram would be a really interesting way to analyze trade data between countries.

It should be noted that what I created isn’t a fully vetted journalistic piece yet. I’ve taken steps to clean the database and ensure the accuracy of the visualization, but I haven’t shown anything to CITES, nor have I fully reported out any outliers or odd trend.

Like all data, CITES data are dirty. First off, the trade reporting the database is based on could be incomplete and in some cases almost certainly is. Also, trade is reported by both countries, but one country’s trade report might not match up with the other’s. That can cause problems.

Here’s how I put it together, in boring detail:

The first step was accessing and understanding the data. I had some familiarity with wildlife trade data from the Convention on International Trade in Endangered Species of Wild Flora and Fauna (CITES) because about four years ago, when I was an intern at National Geographic Magazine, they were working on this investigation into Asia’s Wildlife Trade, and my editor was wrestling with the data.

CITES allows you to download extracts of its data, but it chokes if you try downloading all records for even a year. So getting the whole database, which dates back several decades, wasn’t going to happen (though I have asked nicely and am told by CITES representatives that they might be able to send me bigger extracts). So I knew that if I wanted to get a full year, I was going to have to find a way to download smaller extracts and sew them together. That sounds like a pain, doesn’t it? Well, thanks to a simple Python script, it wasn’t. What I did was download a single csv (comma-separated records) file for different types of trade in the database, which kept the download size within the limit. Then I wrote this basic script ...

