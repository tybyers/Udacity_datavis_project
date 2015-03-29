# Data Visualization with D3.js Final Project

This is the repository for my final project for the Data Visualization with D3.js course, which I am taking as part of the Udacity Data Analyst Nanodegree.

By: Tyler Byers

Date: 28 March 2015

contact: tybyers@gmail.com

## Project Deliverables

This repository contains the following project deliverables:

 * index.html -- Code for the data visualization.  This repo can be downloaded and run on a local server.  Alternatively, the visualization is "live" at: http://bl.ocks.org/tybyers/736da90eefe0c347a1d6.  Note the difference between the code on bl.ocks.org and this repo is the relative reference to the data file.  
 * data/calories_bmi_gdp.csv -- Final data set used for this project
 * data/codebook.md -- Codebook for the data used for the project
 * data/cleaningData.rmd -- R script I used for combining data sets and outputting the final data.
 * data/\*.xlsx -- Data sets downloaded from gapminder.org for this project.

##Summary

This visualization is an animation that shows that people in most countries increased their daily caloric consumption, as well as average body mass index (BMI), between the years 1990 and 2007.  The visualization shows each country as a "bubble" on a scatterplot, where the size of the bubble is related to that country's Gross Domestic Product (GDP) per person.  From the chart, it is apparent that in general the richest countries have the highest daily consumption, as well as the highest BMI, and a careful eye may discern that the richest countries have increased their consumption the most over the 18 years.  In comparison, the poorest countries, especially those in Sub-Saharan Africa, appear to still be struggling with food supply, and may be getting left behind as the richer countries become more and more overweight.   

##Design

###Goal
My goal with the design of this visualization was to show how, over recent years, most of the world's population has seen an increase in body size in tandem with an increase in food supply, and show how this compares to how "rich" a country is.  If I was doing a static chart, I would probably cherry-pick a small number of countries, create a facet plot, and show a scatterplot of BMI versus calorie consumption, encoding the years as colors on the plot. An example of this I did on a similar data set for a different Udacity class is shown near the bottom of one of my [forum posts](http://forums.udacity.com/questions/100169215/gapminder-sugar-consumption-and-male-bmi#ud507).

However, the power of D3.js is the ability to go *beyond* static plots.  So, I chose three variables to plot in a scatterplot, or more specifically a bubble plot.  With each bubble corresponding to an individual country, I encoded the x-axis as daily calorie consumption, the y-axis as average male BMI, and the size of the bubble as relative to that country's Gross Domestic Product (GDP) per capita.  Then, I knew I wanted to animate through the years.  While I had data going back to 1980, I limited the data to the years 1990-2007 (2007 was the final year of data in my data sets).  

###Initial Design

I chose to do all the initial design using the dimple.js library.  Since I have not done any web design in several years, I wanted to focus more on presenting the data rather than trying to climb the steep D3.js learning curve and decide on colors, fonts, etc all at once.  Later in the project, as I became more comfortable, I introduced more D3.js elements.

I initially focused on creating a scatterplot for a single year of data.  When I did this, I noticed that dimple.js was representing the bubble size a little differently than I expected. While GDP per capita should be relative to the area of the circle, dimple.js was using this data to encode the radius directly.  So, for example, a country with a GDP of \$20K per capita had a circle with an area four times the size of a country with \$10K per capita, and sixteen times the size of a country with \$5K per capita (since a circle's area is based on the radius squared).  So, I had to create another data variable that is the square root of GDP per capita, and use that variable to encode the size of the circles (the z-variable).

Once I got that working, I figured out how to animate through the years 1990-2007. I relied heavily on an [animation example](http://dimplejs.org/advanced_examples_viewer.html?id=advanced_storyboard_control) from the dimplejs.org site.  As in the example, the animation control bars also encoded some data -- in this case it was the total number of calories consumed across all countries combined for each year.  For the most part, the animation was working and I thought it was a good start, so I used this as my halfway point and solicited feedback.

A screenshot of my visualization at this point is below:

![Data Vis at midway point](https://lh3.googleusercontent.com/7k9kaHmx-AFBWdju5PTtF0iyYMBfbZKonXdKtCjhjs6N=w634-h332-p-no) 

###Incorporating feedback

I received excellent feedback at the mid-point of my project (see Feedback section).  In particular, Chris Saden from Udacity offered and gave me extremely valuable feedback via email, and I took many of his suggestions. Charlie Turner, also from Udacity, gave me good feedback, and I tried to incorporate some of her ideas into the final visualization.

A list of the changes I made to the visualization after receiving feedback is below.

 * Changed the location of the "Region" legend to on top of the chart to make it easier to find.
 * Allowed the user to filter out the regions they want to see.  This helps a bit with overplotting, but then the bubble size changes depending on the min/max of the GDP in the filtered data.
 * Changed the opacity of the bubbles to 0.6 (default in dimple.js is 0.7 or 0.8). This makes it easier to see the overplotted bubbles.
 * Removed the tooltip when hovering over the year bars.  They were trying to show up in the upper left of the chart, instead of right next to the year bars.  I found out that this "feature" was broken between version 2.0.0 and 2.1.2 of dimple.js (I used 2.1.2 for this visualization).  I couldn't figure out how to fix this feature because it's broken in a "hidden" method.
 * Re-encoded the year bars' data.  Instead of being the sum of all countries' calorie consumption, it is now the average of the countries' consumption for the year.  
 * Put an x-axis for the year bars data.
 * I changed the information in the bubbles' tooltips. They now show: Country, Region, GDP per capita, BMI, and Calorie Consumption. In particular, they no longer show the GDP.sqrt variable. 
 * Added a legend to tell users what the bubble size means.  Because the bubbles change in size depending on what regions are selected, and what year is shown. I could not show "fixed" bubble sizes.  
 * Changed the precison for data on the x-axis in the main chart. Decimal values not important for calorie consumption.
 * Put the source of the data on the bottom of the graphic.
 * Made the title of the chart more descriptive.
 * Put an explanatory paragraph between the title and the chart, so the user has an idea of what the chart is telling them.
 * Thought about my audience. Decided that my audience is readers of an online newspaper, who are reading an article talking about how each year more countries are dealing with problems related to an increasingly obese population, and food-supply/hunger is becoming less of a problem.  Hoping users will play with the chart to learn more.
 * Took Chris Saden's advice to change my code to create a list of the years 1990-2007 using Javascript rather than typing each year out by hand.
 
###Feedback not incorporated

There were some feedback items that I was unable or unwilling to implement.  A list of them is below:

 * Legend with bubble size meanings. I could not easily create a "fixed" bubble size legend, because the bubble sizes change with the min/max of the data shown on each chart, and how it is filtered by the user.  I thought creating a legend that changes with the data would be extremely hard to implement, and might be distracting to the user.
 * Bubbles "whizzing in from bottom left."  This is due to certain countries either joining the data set (see large number of European countries joining after the USSR collaped), or countries dropping out of the data.  Because bubbles zooming in from the origin is default behavior for dimple.js, I could not fix this distracting feature without completely dropping certain countries from the data, which I did not wish to do.
 * More focus on the story of low-GDP countries.  I wasn't sure how to do this, beyond continuing to show how they are sort of being left behind while the rest of the world gets larger.  The user can play with them a bit more by filtering out other regions, but I wanted to leave the user to explore that themselves
 * "Analyze GNI instead GDP." I was happy with my choice of GDP.
 * "Compare this data sets with healthy statistics (e.g. Liver cancer, Sugar per person, Total health spending etc.)."  I thought I had enough information in this visualization.  
 * Overplotting concerns.  There are some ways around this, such as selecting the region, and I changed the bubbles' opacity.  However, without allowing the user to zoom in and out on the data, this is pretty hard to do since there's such a spread in the data between regions that I need a relatively big x-axis.
 
###Final Design

After incorporating as much feedback as I was able or willing, my visualization definitely looks more complete and I believe it meets the criteria for an explanatory graphic. The user is able to filter and view lots of information, but I believe the chart conveys my message of "growing waistlines" fairly well.

A screenshot of the final visualization is below:

![Data Vis final snapshot](https://lh3.googleusercontent.com/wsD1bv8-y5cMHsfsjLiMQBwzy24X0ao0tmkpFEJENXvw=w800-h414-p-no)

As mentioned in the Project Deliverables section, the "live" version of the visualization is found at bl.ocks.org: http://bl.ocks.org/tybyers/736da90eefe0c347a1d6

##Feedback

At the mid-way point of the project, I solicited feedback for the project.   

I received email feedback from two people, and I also received feedback from two people on the Udacity nanodegree forums.  


###Feedback 1
####Chris Saden (Udacity instructor), via email

This graphic is looking great! I have some tips and questions that may help as you continue working on it. I've grouped my feedback below into three categories: the graphic, the user interface, and the code.

At the highest level, I think you’ve done an excellent job of presenting the data in a well chosen chart. To change your graphic from an exploratory graphic to an explanatory graphic, you should think about the main takeaways you want your reader to know about the data. Think about calling out the most important information in the graphic somehow (in the visual encodings, the hierarchy of information on the page, text annotations, title/subtitles, or through use of color and pre-attentive attributes.

On to the details...

**Graphic**

*What’s Great*

 * Well chosen visual encodings and chart type for your data!
 * The regions of the world are colored with a qualitative color palette. ::thumbsUp::
 * The animation is an excellent touch. When I first pulled up the graphic, I see the circles moving, and this draws me into the data and the graphic.
 * You have a descriptive title and units on the axis labels!
 * I like how you have included text annotations regarding the animation and how to stop it.
 * The animation has a nice transition, and I can even see when new countries appear on the screen as the move from the origin to their location when transitioning from year to year in the animation. Nice touch!

*Suggestions*

 * You could move the legend to the top of the graphic and have it span one horizontal line. My eye bounced around to find the legend, and then, my eyes went back to the main data display. It’s bit easier on the reader if they encounter the legend before the main data display. You might also try to order the colors in the legend in the same order that a readers’ eyes would encounter them in the graphic. It helps to reduce cognitive load Simple bar charts and grouped bar charts often do that. Here’s one example.
 * If you can’t customize the legend to your liking using dimple.js, you can try to create your own legend using HTML and CSS. Remember you can create elements on the HTML page and put your graphic in the HTML page. Everything doesn’t have to be in the SVG.
 * Consider creating a legend that gives the reader some reference for the size of the circles.
 * You might try increasing the transparency of the circles. The top right of the graph has many overlapping circles so there are some circles that I can’t hover or click on to drill down into the data. An associated table linked to the graphic could alleviate that problem, but I think that’s way beyond the scope of the class. I have another idea for this problem in the user interface section.
 * What’s the source for your data? I found it on the discussion post, and you can include a small detail in the graphic or in HTML that provides the same information. You can find many examples of this at the bottom corners or just below most graphics (NYTimes, Guardian, Pew Institutes, etc.)
 * What precision do you want on the numerical labels on each axis? The “.0” after all the numbers isn’t needed since it doesn’t reveal more information about the data. The hover you have achieves the more detailed precision.
 * When hovering over the circles, the sqrt of GDP shows. Can you hide this information?

**User Interface**

 * I like how you experimented with including data on the buttons for each year! I’ve actually never seen this before, and I think that was a big risk so I’m glad you did it. There are some drawbacks to doing this, and I’ll explain below in my other comments. I want to commend you on experimenting!
 * When I hover on the year bars, a tooltip appears in the top left of the graphic so maybe that’s something you are working on.
 * The data encoded in the year bars/buttons isn’t as clear as it could be because there’s no baseline or axes to help the reader interpret it. For example, there’s been about 100K increase in Calories Per Person Per Day between 1990 and 2007, which is about a quarter of an inch on the page. That’s the only context I have for the data. I can’t really compare the buttons to determine how the years compare unless I hover to get the detail and compare the numbers in my head (which requires more of my brain power). I think data encoded by the buttons might be better conveyed in a line chart or bar chart in addition to your current graph. The data in the buttons/year bars show a general trend of increased consumption in the world, and it seems to hold true for all countries.
 * One reason I think the year bars/buttons are confusing is that they serve two very different purposes. In one way you are conveying data in the aesthetics of the year bars. In another way, these buttons serve as an interactive element to filter and display the data. This dual purpose might confuse some viewers. Then again, others viewers may get it. Definitely, test this out with other people to get more feedback!
 * Finally, you could add a filter to the graphic that lets viewers toggle on and off circles for a particular region of the world. This also would alleviate the problem of overplaying in the top right graphic. This also let’s the viewer see trends in different parts of the world. For example, It seems like countries within the same regions of the world, generally speaking, have their circles on the same horizontal line so they have about the same average BMI. I might be wrong on this…this is just looking briefly at the animation so I’ll leave it you to see if the data speaks to this. I really want to encourage you to make this addition to the graphic because I know if you put in the effort, you could add this filter and learn a lot in the process.

**Code**

 * Your code is awesome! It’s well structured and has meaningful comments.
 * Great use of a strict equal comparison ( === ). Sometimes, you can get into trouble when not using it.
 * One small thing, look up how to create list of of numbers from 1990-2007 and then convert those numbers to strings. Pushing you to learn more Javascript here.   :)    MDN Javascript is a great resource.

** Back to High Level Feedback** 

 * Think deeply about what you want people to learn from your graphic. Do you want them to know about specific comparisons or general trends? How can you call those pieces out in your graphic?
 * The title tells me the what of the graphic but it doesn’t explain key findings in the data. Tell the reader what they should know and why it’s important. Don’t make them search for it.
 * Finally, think about who your audience would be for this graphic. If you don’t have an audience in mind, make one up (presenting to a board at the World Health Organization, the general public, a committee concerned about overpopulation and world food shortages).
 * Does your audience have familiarity with the terminology/data? Do you need to define anything or add context?
 * Here are two articles that I think you’ll find helpful in polishing your visualization. Remember to move your graphic from an exploratory graphic to an explanatory graphic as this is what data scientists and analysts do when communicating findings to others. There’s certainly a place for exploratory graphics, but remember that you are telling a specific story since you’ve spent so much time with the data already.
 ** http://www.storytellingwithdata.com/2014/07/lead-with-story.html 
 ** http://www.storytellingwithdata.com/2011/04/good-chart-takes-time.html 

As the title of the second link indicates, a good chart takes time. I think you’re most of the way there already, and I’m excited to see the final version!

Chris

###Feedback 2
####Ann Byers, via email

This is pretty cool, doing a 3 dimensional project with 2 axis - using the 3rd with size of circles

I notice the obvious of yearly shifting, but when the Iron curtain was lifted, those countries increased in BMI, probably having more food (or maybe data wasn't available prior to)
Is the purpose of this to show that larger countries can produce more food and thus feed there people more (other than Japan and China)
Seems to be the larger countries eat more. There is also a possible observation that is BMI tied to culture/genetics
The desert countries eat less, have lower BMI's
Why do the fat countries stay fat with all the education on nutrition. Apparently the higher the education, doesn't necessarily correlate to wiser choices in taking care of ourselves.  :)

###Feedback 3
####alex_293710221 (fellow Udacity student), on Nanodegree forums
There is really cool graph. As for me, your data is clear for understanding. 

I see the general trend is growing worldwide food consumption and BMI.

Main relationship is BMI extremely high mostly in countries with food consumption more than 2600 calories per person.

America have a big dispersion of food consumption. 

Another fact is Sub-Saharah Africa region is stay on the same place of food consumption and fewer than 2200 calories. It is too small. Sad.

As an option, you can analyze GNI instead GDP. Maybe it can also show interesting relationships. 

Another possible case is compare this data sets with healthy statistics (e.g. Liver cancer, Sugar per person, Total health spending etc.)

###Feedback4
####Charlie Turner (Udacity instructor/coach), on Nanodegree forums

I'm one of the evaluators for this project, but the comments I give here will be outside of that role, for feedback/learning/improvement purposes rather than giving an indication of whether your project fits the rubric or not. I'm sorry to be so formal about that -- I just want to give you my free personal view here, rather than discussing your work in light of the specifications for now. I hope that makes sense, and I (and other Coaches) would also be happy to answer questions about the rubric/evaluation standards if you have them.

Firstly - I think this is a very nice graphic!

The first thing I notice is the movements of circles. I think that's pretty natural, for the eye to be caught on these. To allow me to concentrate on what's being shown, I think I would prefer the visualisation to stop when it hits the end of the years, in order for me to look more closely. 

The circles that whizz in from the bottom-left corner particularly caught my eye. I am not sure whether they are new countries that aren't included in some years, or whether they are countries that see sudden increases in BMI and calorie consumption, but they definitely stood out - it may be worth considering whether you want the eye to be drawn to these more than others.

My question was "what does circle size mean?" I guessed from the title and tooltip that this is GDP per capita. You should definitely include a key to help the viewer interpret this. I also wondered whether information was obscured by overplotting of circles. Being able to select certain subsets (continents?, countries?) might be useful to solving this.

The biggest thing I noticed was a general movement "up and to the right" - this comes out clearly when the visualisation loops back to 1990. I guess I was particularly interested in countries that don't follow that trend, but the visualisation was moving a bit too quickly to follow those properly.

It was clear that some continents are eating far less than others and that low GDP and low BMI and low calorie consumption go together.

The small size of the circles countries with low GDP gives them less 'importance' in the graphic - the eye is naturally drawn to the larger circles. It might be interesting to consider how to bring out the stories of countries with low GDP, too.

I think that tooltips whilst the visualisation is moving are not working too well, they get left behind as the animation moves on. It would be nice if it were a little easier to pause/stop the visualisation in order to then hover and use the tooltips. It might also be a good idea to adjust the tooltip itself so that it shows GDP per capita correctly, rather than its square-root - this is not intuitive to interpret!

I'm not sure what the little box in the top left corner does, it appears when I hover on a year (I think) but it's kind of half-hidden so I can't read it.

If you want to bring out the stories in the data, don't be afraid to point things out with text on the page! If you've spotted something interesting, share it!

Overall, I like your visualisation. I think you've chosen a sensible number of variables and encoded them well. I'm pleased that you've fixed your axes and have the dots moving, rather than adjusting axes too! The animation definitely tells the story here. 

I would like the option to explore the data in more detail, and a little more guidance (you're the expert here!) about what to look for in the data. My concerns are about overplotting, ease of use regarding animation and tooltips, and about missing out on the small-GDP countries.

##Resources/References

###Data

All data from www.gapminder.org

GDP/capita(US$, inflation-adjusted): https://spreadsheets.google.com/pub?key=0AkBd6lyS3EmpdHo5S0J6ekhVOF9QaVhod05QSGV4T3c&gid=0

Body Mass Index (BMI), men, Kg/m2: https://spreadsheets.google.com/pub?key=0ArfEDsV3bBwCdF9saE1pWUNYVkVsNU1FdW1Yem81Nmc&gid=0

Sugar per person (g per day): https://spreadsheets.google.com/pub?key=phAwcNAVuyj2sdmdhX9zuKg&gid=0

Food supply (kilocalories / person / day): https://spreadsheets.google.com/pub?key=0ArfEDsV3bBwCdGlYVVpXX20tbU13STZyVG0yNkRrZnc&gid=0

World Regions: https://spreadsheets.google.com/pub?key=phT4mwjvEuGBtdf1ZeO7_PQ&gid=1

###References

Udacity Data Visualization with D3.js course: https://www.udacity.com/course/ud507

Dimple.js: http://dimplejs.org/index.html . Special mention:

 * Storyboard Control example:http://dimplejs.org/advanced_examples_viewer.html?id=advanced_storyboard_control
 * Interactive Legend: http://dimplejs.org/advanced_examples_viewer.html?id=advanced_interactive_legends
 * Custom Tooltips: http://dimplejs.org/adhoc_viewer.html?id=adhoc_bar_custom_tooltips
 * Dimple wiki: https://github.com/PMSI-AlignAlytics/dimple/wiki

D3.js: https://github.com/mbostock/d3/wiki

_Interactive Data Visualization for the Web_. Murray, Scott. Available: http://chimera.labs.oreilly.com/books/1230000000345/

Stackoverflow:
 
 * Several quick syntax checks on www.stackoverflow.com. Did not keep track of all the sites.
 * http://stackoverflow.com/questions/25416063/title-for-charts-and-axes-in-dimple-js-charts