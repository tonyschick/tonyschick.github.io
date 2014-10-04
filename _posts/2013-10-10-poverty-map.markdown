---
layout: post
title:  "Creating and mapping a rate to compare to the federal poverty measure"
date:   2013-10-10 12:19:00
categories: jekyll update
---

<iframe frameborder="0" scrolling="no" width="100%" height="640" src="http://a.tiles.mapbox.com/v3/tonyschick.road-trip/page.html#4/40.25/-88.95"></iframe>

One of the main tasks within a project I’ve been working that I’ve dubbed “Poorly Defined” -- a year-long writing fellowship covering poverty funded by the Missouri School of Journalism -- is using data that’s compiled on “living wages” to create a rate that can be compared to the official poverty rate. Most people look at the official poverty thresholds, which haven’t been updated in nearly 50 years, and struggle to understand how a single person could get by on, say, $18,000, let alone how a single parent of 3 could get by on $18,000 in New York City. For a great simplified explanation of this, check out [this brief story from a recent episode of NPR’s Planet Money.](http://www.npr.org/blogs/money/2013/08/27/214822459/a-college-kid-a-single-mom-and-the-problem-with-the-poverty-line)

In recent years, nonprofit groups, sociologists and economists have been developing new thresholds that better estimate the cost of living in the U.S., that include work-related expenses and child care, and that -- perhaps most significantly -- adjust for geographic differences in cost of living. 

Efforts include the Self-Sufficiency Standard from researchers at the University of Washington, the Family Budget Calculator from the Economic Policy Institute, Basic Economic Security Tables from Wider Opportunities for Women and The Living Wage Calculator from the Massachusetts Institute of Technology.

My aim, which I’d included in my original pitch to the University of Missouri and later included in a pitch to The Investigative Fund of the Nation Institute, was to use one of these well-established thresholds to create a rate we could compare to the poverty rate, on a national level and for different locations. 

Our first charge was to figure out which measure to use. All of them are fairly similar, but we needed to decide which one we would rely on.

The Self-Sufficiency Standard, created by Diana Pearce, has been around the longest and is the most detailed, as it’s calculated for more than 60 family types. But, it’s calculated on a per contract basis, so it’s only been created for about 37 states, and many of those standards are several years out of date. The Basic Family Budget Calculator has been calculated for far fewer family types and presents similar geographic challenges. We ultimately decided on the Living Wage Calculator: It comes from MIT, a trusted institution, has a published methodology, was updated within the past year, has been widely cited and has stood up to scrutiny, and has been calculated for every county in the U.S., meaning we could do a fairly detailed and consistent analysis across the country.

So we had our threshold -- half of the equation for calculating a poverty rate -- and it was created for us. The other half we needed was a population’s worth of income data, and we needed real families’ incomes so that we could apply the right threshold to each one. 

So we turned to the Public Use Microdata Sample (PUMS). 

PUMS is a sample of actual responses, not aggregate statistics, within the Census Bureau’s American Community Survey. It’s a trove of information that can be used to determine things like what former Oregonians are doing in Missouri or how many public school teachers send their kids to private school.

To get the dataset we needed, I had to code the families in PUMS into the 8 family types created in the Living Wage Calculator (having only 8 family types, this somewhat underestimates the cost of living for families with more than 3 children, though the threshold is still much higher than the official poverty line).

This required some judgment calls, though. What constitutes a family and what doesn’t? The official poverty measure has a fairly traditional definition: If you’re an unmarried partner, roommate or non-immediate family member, you’re an individual unit, separate from the family you might live with. 

Parsing the families this way was one option. The other was assuming that all members of a household, regardless of relationship, share resources to some degree rather than not at all. 

I decided to try coding it both ways and realized the difference was negligible, much smaller than the margin of error in each sample, and choosing one over the other would ultimately not have a meaningful affect on  the outcome of the analysis. So to save time, I went with all members of a household.

Determining household type required knowing the number of adults and children in each household. The official measure differentiates between individuals above and below age 18. Because the Living Wage Calculator includes child care as a not insignificant cost, that differentiation makes little sense. I decided to consider any household member age 14 or above and without a self-care disability to be an adult (PUMS has fields listing whether an individual has certain disabilities). This prevented us from applying child care costs to households without individuals requiring child care. 

These are judgment calls, always tough in an analysis.As I went about making these decisions, I spoke with analysts from other projects such as the Self-Sufficiency Standard and red technical papers and spoke with representatives from the Census Bureau.

But PUMS presented another challenge. The main limitation of the dataset is geography. For privacy purposes the most precise geography available is called a Public Use Microdata Area (PUMA). These are designed to to include at least 100,000 people and thus in some cases are smaller than counties and in some cases are much larger. The areas within each PUMA tend to be demographically and economically similar, but of course there is some variation.

So how did we reconcile county-level thresholds with PUMA-level incomes? We turned to John Blodgett of the Missouri Census Data Center, the University of Missouri organization that created a geographic conversion tool.As it turns out, arguably the country’s leading expert on conversions between these boundaries worked on the same university campus I did. 

Blodgett walked me and an interested colleague through how to take weighted averages of the county thresholds and disperse them to the PUMAs. So what we ended up with were PUMA-level thresholds based on averages from the counties, which gave us an accurate and defensible representation.

Once we had both the incomes and the thresholds, it was simple math and crosstabs to determine whether a household was above or below the living wage line and ultimately to determine the rate for each PUMA. (I started doing this in the R statistical language but eventually switched to SPSS software. It crunched the numbers faster, plus R was a new language for me. The analysis alone was complex enough. I didn't need to throw a new language on top of it)

Getting those calculations was a triumphant moment, but I soon realized it didn’t mean anything.

I don’t know where or what area 0100200 is (well, truthfully by now I know it’s somewhere around Autauga County, Alabama, but you get the point). To actually make sense of the calculations, I had to either a) convert it back to counties or b) map it. I figured if we could take the county data and convert it to PUMAs, then why couldn’t we do the reverse and go back again? 

So I did that. And I made a stupid mistake. Doing that told me Oconee County, Georgia, had the highest difference between the poverty rate and the below-living-wage rate. So by my measure, that means Oconee County has the highest number of uncounted poor. 

Google Oconee County. That doesn't pass the sniff test.It’s one of the most prosperous counties in Georgia. 

What happened? Well, Oconee County has a relatively low poverty rate but it's surrounded by poorer counties. None of them are densely populated, so they are grouped into one PUMA with a relatively high rate of people below the living wage threshold. When I converted it back to counties, Oconee was assigned that high rate, which wasn’t an accurate representation of it.

So, that wasn’t going to work. 

Mapping, then, was the best way for me to understand the data spatially. Using Quantum GIS, TileMill and Mapbox, [I created this map](http://a.tiles.mapbox.com/v3/tonyschick.road-trip/page.html#4/40.25/-88.95), a “chloropeth” map shaded by the rate of people below the living wage threshold. You can see clusters of high disparity in urban areas like New York, Chicago, Atlanta, the San Francisco-Oakland Bay Area and Los Angeles, all of which have a newly calculated rate more than 20 percentage points higher than the official poverty rate. 

The next step is reviewing the map with editors to determine the best places for on-the-ground reporting.

-- _Tony_

