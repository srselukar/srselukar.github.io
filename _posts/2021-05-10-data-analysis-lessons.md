---
layout: post
title: "Lessons Learned for Data Analysis"
author: subodh
date: 2021-05-10
tags: stats
categories: Statistics
---
    
I've had the opportunity to work on a variety of data analysis projects so far, and I wanted to make post about a few lessons I've learned so far. Of course, there is so much more to learn, and I'm interested to see how this list changes over time.

1. There is a value in taking a break and stepping away from a problem after thinking about it for a while.

Once I get the motivation to work on a task, I really want to get the whole job done - in one sitting, if at all possible. That's great for timeliness, and it can be very useful when working on a project that is iterative and collaborative - when putting any ideas together is the top priority.

However, at other times, there is an immense benefit in taking it more slowly. When developing a data analysis plan or when coding it up, I've improved my ideas and my code just by stepping away for even a short period. A given analysis may make certain unlikely assumptions that I didn't catch the first time around, or maybe a piece of code incorrectly sweeps some missing data aside. Switching to a different project or taking a break and then returning to the problem has helped me to catch things like that.

2. Don't overshare the technicalities.

A lot of the the statistical training that I've had has been about being as precise as possible. 

As such, sometimes I have to actively fight the urge to explain every detail when communicating statistics; otherwise, it can have the result that my main conclusions go overlooked behind a list of possibly-overly technical assumptions.

The most technical details can be important for sharing internally or for presenting to a statistically-savvy audience, but the strategy that I've learned for other audiences is to focus on the top-line results with any salient caveats. Other details can be put into footnotes or appendices as necessary. I'm still learning where the line lies and how to make these choices!

3. When coding, think hard about the input data and the anticipated output.

PhD coursework focuses a great deal on having a solid understanding of how statistical methodology works, but what goes in and what comes out is also critically important.

For me, this has come up a lot with calculated variables as input and with missing data. 

R frequently ignores missing data, which means the analysis method may make implicit assumptions about these data. I've learned it's prudent to simply check the input and output sample size to make sure there's no unexpected missing data! Appropriate handling of missing data is a difficult issue, but acknowledging its existence is always the first step to addressing it.

Calculated variables can be messy because they introduce multiple layers for incorrect analysis. There is always a chance that the original data were recorded incorrectly/biased, and now an intermediate step is a new source of error. 

In one of my projects, the recorded data were daily bleeding entries, and the outcome of interest was the indication of any serious bleed within a fixed time period. This seems straightforward, but it requires (1) addressing missing bleeding entries and (2) summarizing across the bleeding entries in the time period. It took a few iterations before I got all of the details right! And that's before the actual analysis that was presented in the results.


