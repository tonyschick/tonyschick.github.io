---
layout: post
title:  "Visualizing wildlife trade data"
date:   2013-09-24 12:19:00
categories: jekyll update
---

<a href="http://evening-meadow-8175.herokuapp.com/projects/wildlife/" target="_blank"><img style="width: 100%" src="/imgs/wildlife.png" /></a>

I’ve been wanting to use wildlife trade data for a long time. Wildlife trafficking fascinates me. I’ve also been looking for a data viz project, because after seeing it in action and reading/hearing about how great the javascript library is for working with data, I’ve been eager to build something of my own with D3js.

Putting the two together was pretty fun. [ Here's a link to the visualization on my old site. ](http://evening-meadow-8175.herokuapp.com/projects/wildlife/)

What I originally wanted to do was access the full database and build a web application that allowed users to search trades over time as well as view visualizations of trade trends, trades between countries, and traffic for each species. This would have been a really useful tool for reporting on this subject, too.

But I can’t do that yet, because I don’t have full access to the database (more on this below). Right now, the visualization shows live wildlife trade for 2011, the latest year available. 

The next logical step is the addition of non-live trade such as animal parts, which is a little trickier because some of them are measured in units, some in milligrams, some in other metrics, etc. So once I clean that up and figure out how to aggregate the data given the various units of measurement, you’ll be able to see that here as well.

I opted to create an initial visualization and build on it when I could. The database is vast enough and my idea lofty enough that if I waited for everything to be right, I'd never dive in. 

Looking through the D3 examples of different visualizations, I realized the chord diagram would be a really useful way to analyze trade data between countries. (The example shows debts between countries).

I feel compelled to offer this disclaimer: what I created isn’t a fully vetted journalistic piece. I’ve taken some steps to clean the database and ensure the accuracy of the visualization, but I haven’t shown anything to CITES, nor have I fully reported out any outliers or odd trends. I'm posting it as a experiment into what can be done with this data and with D3. So please, if you want to draw conclusions about international trade, don't use this. Go directly to CITES. 

Like all data, CITES data are dirty. Really pretty dirty. First off, the trade reporting that the database relies on could be incomplete. In some cases it almost certainly is. Also, trade is reported by both countries involved (importer and exporter), but one country’s trade report might not match up with the other’s. Oh what fun we're having.

Here’s how I put it together, in boring detail:

I had some familiarity with wildlife trade data from the Convention on International Trade in Endangered Species of Wild Flora and Fauna (CITES) because about four years ago, when I was an intern at National Geographic Magazine, they were working on this investigation into Asia’s Wildlife Trade, and my editor was wrestling with the data.

CITES allows you to download extracts of its data, but it chokes if you try downloading all records for even a year. So getting the whole database, which dates back several decades, wasn’t going to happen (though I have asked nicely and am told by CITES representatives that they might be able to send me bigger extracts).

I knew that if I wanted to get a full year, I was going to have to find a way to download smaller extracts and sew them together. That sounds like a pain, doesn’t it? Well, thanks to a simple Python script, it wasn’t. What I did was download a single csv (comma-separated records) file for different types of trade in the database, which kept the download size within the limit. Then I wrote this basic script ...


		import pandas
		from pandas import *
		import numpy
		 
		# abbreviate the pandas module for ease of scripting
		pd = pandas
		 
		# read the various csv files as variables
		# these are the csv files we downloaded one by one
		# because of the site's download size restrictions
		 
		be = pd.read_csv("data/2011compare_be.csv")
		 
		ghlm = pd.read_csv("data/2011compare_ghlm.csv")
		 
		q = pd.read_csv("data/2011compare_q.csv")
		 
		s = pd.read_csv("data/2011compare_s.csv")
		 
		z = pd.read_csv("data/2011compare_z.csv")
		 
		compare2011 = pd.concat((be, ghlm, s, z), axis=0)
		 
		compare2011.to_csv("2011compare.csv")
		 
		print "All done!"

]... and while I was filling up my water bottle it was stitching together my data. Let’s walk through it step by step.

import pandas
from pandas import *
import numpy

This saying “Hey, import these pre-made packages. We’re going to use some of their stuff.” To run this script, you’ve got to have pandas and numpy installed. They are tools that make it easier to do math and data science using Python. They make it easier to do what we do later on.

pd = pandas

All this does is abbreviate pandas to pd. For a script this small, it’s not really necessary. It just makes it faster to write later on, and it’s how I learned it, so I always write it because I’m used to writing “pd” rather than “pandas” later on.

be = pd.read_csv("data/2011compare_be.csv")

This is telling the script we’ve got a new variable that we’re going to store some information in. So it says “hey there, we’ve got a new variable called ‘be’ and inside ‘be’ you’re going to store whatever information you get out of the following command. The following command happens to be one called “read_csv” and “read_csv” doesn’t just exist everywhere, it exists within the package known as pandas. That’s why we have to import pandas, and from pandas we have to import everything (the asterisk is a symbol for all in the code above). So, “read_csv” is built to understand a comma-separated file, and all we have to do is tell it where the file is. I repeated this for each of the files.

compare2011 = pd.concat((be, ghlm, s, z), axis=0)

This says “create a new variable and that varialbe will be equal to all the other variables added together”. Concat, in this context, vertically stacks the data because we specified the axis of 0. If we specified an axis of 1, it would append each file as a new set of columns rather than a new set of rows.

compare2011.to_csv("2011compare.csv")

Save what we just made as a new csv file.

Once I had the csv of all the records for 2011, I still had a little cleaning to do. The first thing I had to do was aggregate it. I found out the hard way, by screwing it up, that the javascript I was using to visualize the data couldn’t process it correctly if it had multiple enries, like this:

u.s., britain
u.s., china
u.s., russia,
u.s., britain

So I ran a pivot table. Then, I wanted actual county names, rather than the two letter country code, so I had to create a separate table for this, which I downloaded from CITES. I then imported it all into MySQL so that I could do a join and make sure the right full country names were connected to the right country codes. Yes, I could have done this just using the Python language, but I thought it would be a good idea to have my data in a database.

Once I had the aggregate data and the proper file names, I was ready to start the visualization. To learn how to use D3, I downloaded a book (it was free) from the very helpful O’Reilly , called [Interactive Data Visualization For the Web](http://chimera.labs.oreilly.com/books/1230000000345).

I ran through it once and found D3 to be not only one of the most helpful but one of the most intuitive javascript libraries I’ve found. It’s incredibly powerful, and its abilities go way beyond what I’m capable of producing, and its depths are way beyond what I can understand at this point. But, as far as working with data in a browser, creating visualizations and interactivity, D3 makes a lot of sense.

Here's the full D3 script, which I tried to annotate as best I could. Full disclosure: some of this was borrowed from examples at [d3js.org](http://d3js.org):

If any of it doesn't make sense but you'd like it to, or you have a problem with some of it you think I should change, let me know. You can contact me through the links at the side of the page.

-- _Tony_

Chart dimensions.
		        var w = 1200,
		            h = 1000,
		            r1 = Math.min(650, 650)/2,
		            r0 = r1 - 20,
		            format = d3.format(",.3r");
		 
Square matrices, asynchronously loaded; exports is the transpose of imports.
		        
		        var imports = [],
		            exports = [];
		 
The chord layout, for computing the angles of chords and groups.
		        var layout = d3.layout.chord()
		            .sortGroups(d3.descending)
		            .sortSubgroups(d3.descending)
		            .sortChords(d3.descending)
		            .padding(.025);

The arc generator, for the groups.
		        
		        var arc = d3.svg.arc()
		            .innerRadius(r0)
		            .outerRadius(r1);
		 
The chord generator (quadratic Bézier), for the chords.
		        
		        var chord = d3.svg.chord()
		            .radius(r0);

Add an SVG element for each diagram, and translate the origin to the center.
		        
		        var svg = d3.selectAll("body").selectAll("section")
		            
				.data([imports, exports])
				.enter().append("div")
				.style("display", "inline-block")
				.style("width", w + "px")
				.style("height", h + "px")
				.append("svg:svg")
				.attr("width", w)
				.attr("height", h)
				.append("svg:g")
				.attr("transform", "translate(" + w / 2 + "," + h / 2 + ")");

Load our data file. Which, I'm being pretty lazy about just loading from Dropbox:

		        d3.csv("https://dl.dropboxusercontent.com/u/24686053/wildlife_live3.csv", function(data) {
		          var countries = {},
		              array = [],
		              n = 0;
		 
Compute a unique id for each country.

		          data.forEach(function(d) {
		            d.Importer  = country(d.Importer);
		            d.Exporter = country(d.Exporter);
		            d.valueOf = value; // convert object to number implicitly
		          });
		 
		 
Initialize a square matrix of imports and exports.

		          for (var i = 0; i < n; i++) {
		            imports[i] = [];
		            exports[i] = [];
		            for (var j = 0; j < n; j++) {
		              imports[i][j] = 0;
		              exports[i][j] = 0;
		            }
		          }
		 
Populate the matrices, and stash a map from id to country.

		          data.forEach(function(d) {
		            imports[d.Exporter.id][d.Importer.id] = d;
		            exports[d.Importer.id][d.Exporter.id] = d;
		            array[d.Exporter.id] = d.Exporter;
		            array[d.Importer.id] = d.Importer;
		          });

For each diagram…

		          svg.each(function(matrix, j) {
		            var svg = d3.select(this);

Compute the chord layout.

		            layout.matrix(matrix);
		 
		            svg.insert("text")
		                .text(function(d) { return (j ? "Imports " : "Exports "); })
		                .attr("class", "splainerhead")
		                .attr("x", -450 + "px")
		                .attr("y", -450 + "px")
		 
Add the chords to the svg:

		            svg.selectAll("path.chord")
		                .data(layout.chords)
		              .enter().append("svg:path")
		                .attr("class", "chord")
		                .style("fill", function(d) { return fill(d.source.value); })
		                .style("stroke", function(d) { return fill(d.source.value); })
		                .attr("d", chord)
		                .append("svg:title")
		                .text(function(d) { return format(d.source.value) + " live animals " + "from " + d.source.value.Exporter.name + " to " + d.source.value.Importer.name; })
		 
Add groups.
		            var g = svg.selectAll("g.group")
		                .data(layout.groups)
		                .enter().append("svg:g")
		                .attr("class", "group")
		                .style("cursor", "pointer")
		                .on("click", fade(.01))
		                .on("dblclick", fade(1))
		 
		 
Add the group arc.
		            g.append("svg:path")
		                .style("fill", "#333")
		                .attr("id", function(d, i) { return "group" + d.index + "-" + j; })
		                .attr("d", arc)
		                .append("svg:title")
		                .text(function(d) { return array[d.index].name + " " + (j ? "imported " : "reportedly exported ") + format(d.value) + " live animals in 2011"; })

Add tick marks and labels for each country:

		            var ticks = svg.append("g")
		              .selectAll("g")
		              .data(layout.groups)
		              .enter().append("g")
		 
		            ticks.append("text")
		                .each(function(d) { d.angle = (d.startAngle + d.endAngle) / 2; })
		                .attr("dy", ".35em")
		                .attr("text-anchor", function(d) { return d.angle > Math.PI ? "end" : null; })
		                .attr("transform", function(d) {
		                  return "rotate(" + (d.angle * 180 / Math.PI - 90) + ")"
		                      + "translate(" + (r0 + 45) + ")"
		                      + (d.angle > Math.PI ? "rotate(180)" : "");
		                })
		                .text(function(d) { return array[d.index].name; })
		                .style("font-size", "10px")
		                .style("font-family", "Verdana")
		                .style("padding", "2px")
		                .style("cursor", "pointer")
		                .on("click", fade(.01))
		                .on("dblclick", fade(1)) 
		 
		 
		 
		                
Create a function to fade out the arc,  to be applied to all countries except for the one selected.

		        function fade(opacity) {
		          return function(g, i) {
		                  svg.selectAll("path.chord")
		                      .filter(function(d) {
		                        return d.source.index != i && d.target.index != i;
		                      })
		                    .transition(30)
		                      .style("opacity", opacity);
		                }
		        }
		 

Add the label, and on it apply a mouseover and mou
		            g.append("svg:text")
		               // .attr("x", 0)
		               // .attr("dy", 0)
		               // .append("svg:textPath")
		               // .attr("xlink:href", function(d) { return "#group" + d.index + "-" + j; })
		               // .text(function(d) { return array[d.index].name; })
		               // .on("mouseover", fade(.1))
		               // .on("mouseout", fade(1));
		            });
		 
Memorize the specified country, computing a unique id.
		            
		            function country(d) {
		              return countries[d] || (countries[d] = {
		                name: d,
		                id: n++
		              });
		            }
		 
		 
		            function value() {
		              return +this.Quantity;
		            }
		 
		        });
		 




