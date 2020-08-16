---
title: "When to Buy"
author: subodh
date: 2020-08-14
layout: post
tags: stats sims
categories: Statistics
output:
  md_document:
    variant: markdown_github
    preserve_yaml: TRUE
---

When should you buy food on sale?
=================================

My roommate asked me to “buid him a statistical model” to figure out
when to buy chicken to minimize his cost. As a vegetarian, it’s probably
a bit unethical to help figure out how to optimally buy chicken, but it
did sound like a decent first post.

My first understanding of the problem as phrased was a simple
optimization problem: minimize the cost at a given store run subject to
having some max storage and a minimum amount of chicken to eat for the
week by deciding how much to buy.

Speaking further, I realized he wanted what I realized was to have some
decision rule to minimize the long-run cost based on some knowledge of
the cost process over time. My reaction to that was that that sounded
like something that a operations research/forecasting expert would be
doing for a lot of money.

But I figured that we could simplify the problem by first limiting the
time period to be costs in the next year and then considering only a
simple decision rule:

1.  Is there enough to last til the end of the year? If yes, don’t buy
    anything.
2.  If no, is the price lower than some cutoff *c*? If no, then buy the
    minimum need to last the week. If yes, then buy the maximum to fill
    the freezer or to last til the end of the year.

``` r
weeklyUse <- 4
maxStore <- 40

weeks <- 52

ytFun <- function(dec,y0,tElaps,d0=weeklyUse,d1=maxStore,maxT=weeks) {
    ifelse(y0-d0*(maxT-tElaps) > 0, # if storage is enough to last out the year
           0, # do not buy, else need to buy
           ifelse(dec, # if price is low
                  min(d1-y0,d0*(maxT-tElaps)-y0), # buy as much as you can
                  ifelse(y0-d0 < 0,d0-y0,0)) # otherwise buy the minimum you need
    )
}
```

Of course, there are more elegant rules in which you don’t opt for only
the minimum or the maximum, but I figured that would do for a Saturday
afternoon. This rule has the ease in that we only need to optimize over
the cutoff and check if the “optimum” cutoff seems roughly robust to
different choices of price distribution.

Now, to actually answer the question, I wanted to take a
simulation-based approach.

1.  Make different choices of cutoffs
    1.  Fixed cutoffs of \$2,…,\$7
    2.  Evolving cutoff where you compare against the minimum price seen
        so far or the average price so far
2.  Generate many “years” (I just did 1000 this time), each year having
    52 prices (representing weeks)
3.  For each year and each cutoff, loop through each week to simulate
    store runs (this is very inefficient, forgive me!) and calculate the
    costs of the year for that cutoff
4.  Average over all of the “years” for each cutoff
5.  Determine what cutoff minimized the average costs!

It turned out that using the evolving average decision rule minimized
the cost across the two scenarios I tried: 1. The costs were \$2.50,
\$4.00, \$6.00 and \$8.00 with probability proportional to 2, 10, 20 and 20
times per year. 2. Gamma distribution with rate 1 and shape 7 (to have a
mean of \$7.00); I truncated it to be between \$2.00 and \$10.00

The rest of the code I used is below. I’m sure this is a very dirty
approach, but intuitively I’m pretty happy recommending using the
average since it’s generally a nice statistic.

``` r
set.seed(2020)

p <- seq(2,7) # grid of rules

reps <- 1000
costMat <- matrix(ncol=length(p),nrow=reps)
costMatUpdate <- matrix(ncol=2,nrow=reps)



# avgP <- 7
# ptExtra <- rgamma(weeks*reps*10,shape=avgP,rate=1)
# ptAll <- ptExtra[ptExtra > 2 & ptExtra < 10][1:(weeks*reps)]

ptAll <- sample(c(2.5,4,6,8),weeks*reps,replace=TRUE,prob=c(2,10,20,20)/52)


for (i in 1:reps){
    pt <- ptAll[((i-1)*weeks+1):(i*weeks)]
    yt <- matrix(nrow=weeks,ncol=length(p))
    ytUpdate <- matrix(nrow=weeks,ncol=2)
    
    tmpStore <- tmpStoreUpdate <-  0
    
    yt[1,] <- ytFun(pt[1] <= p,0,rep(0,length(p))) # start off with 0 at y0
    ytUpdate[1,] <- ytFun(c(FALSE,FALSE),0,c(0,0)) # start off with auto-buying the minimum, start with 0
    for (t in 2:weeks){
        tmpStore <- yt[t-1,]+tmpStore-weeklyUse
        tmpStoreUpdate <- ytUpdate[t-1,]+tmpStoreUpdate-weeklyUse
        
        upd1 <- pt[t] <= min(pt[1:(t-1)]) # is it smaller than the smallest i've seen
        upd2 <- pt[t] <= mean(pt[1:(t-1)]) # is it smaller than the average i've seen
        
        yt[t,] <- ytFun(pt[t] <= p,tmpStore,rep(t,length(p)))
        ytUpdate[t,] <- ytFun(c(upd1,upd2),tmpStoreUpdate,c(t,t))
    }
    
    ct <- yt*pt
    ctUpdate <- ytUpdate*pt
    costMat[i,] <- colSums(ct)
    costMatUpdate[i,] <- colSums(ctUpdate)
}

avgCosts <- colMeans(costMat)
# which.min(avgCosts)

avgCostsUpdate <- colMeans(costMatUpdate)
# which.min(avgCostsUpdate)
```
