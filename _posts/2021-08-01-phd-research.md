---
layout: post
title: "PhD Research Summary"
author: subodh
date: 2021-08-01
tags: stats
categories: Statistics
---
    
I'm gearing up for my job search and have been working on summarizing my current research and possible ideas for future research.

# Dissertation Research
	My dissertation research has been motivated by three contemporary problems in clinical trial design, conduct and analysis. 
	
### Platform Trials with Differing Experimental Arm Eligibility
	In oncology, the LEAP trial (NCT03092674) was a platform trial for acute myeloid leukemia in older adults conducted by the NCI-funded SWOG Cancer Research Network. The trial evaluated several therapies with varying mechanisms of action, including  immunotherapies and targeted agents. Because of these varying mechanisms, certain participant sub-populations were thought to potentially be harmed by specific therapies, so eligibility necessarily differed across arms. For example, patients with pre-existing autoimmune diseases were precluded from receiving checkpoint inhibitor immunotherapy. However, trial investigators did not wish to modify trial-wide eligibility, as a key desire for the trial was to be as inclusive as possible.
	
	The investigators chose to implement stratified randomization, due to the smaller size of the study, but existing methods for stratified randomization would have required the investigators to limit the trial-wide eligibility to recruit only subjects eligible to all experimental arms, which would have impacted study accrual and generalizability. 
	
	In this project, we extend conventional methods for stratified randomization to appropriately account for differing experimental arm eligibility without restricting the trial-wide eligibility. By extending conventional methods, we allow researchers to use familiar tools and software, while facilitating the design and conduct of more flexible studies.
	
	In addition to proposing methods for stratified randomization, we also evaluate the efficiency of platform trials when participants may differ in experimental arm eligibility. Because platform trial efficiency arises out of the use of a common standard of care arm, we derive a formula for the probability of randomization to the standard of care arm based on anticipated participant experimental arm eligibilities. Researchers can evaluate the efficiency of different trial plans with this formula to better allocate trial resources.
	
### Sequential Monitoring in N-of-1 Trials
	N-of-1 trials randomly assign a single participant to a sequence of crossovers between two or more interventions. A common design feature of N-of-1 trials is a block structure: a requirement that treatment sequences be organized with repeated blocks that contain fixed numbers of each intervention. 
	
	In this setting, if the participant refuses to continue, then the entire study ends - and if this decision is made after looking at the data, then the results of the trial can be invalid. Appropriate sequential monitoring is a well-developed part of the literature for group clinical trials, but it has yet to be implemented for N-of-1 trials. This could be because classical sequential monitoring procedures frequently appeal to large-sample theory and a specific independence structure, but such conditions may not seem reasonable in N-of-1 trials. 
	
	In this project, we demonstrate that treatment blocks satisfy conditions to serve as independent units for use with classical sequential monitoring boundaries when analyzing with a linear mixed effects model. Further, we show that nominal type-1 error control can hold for this approach under a range of real-world settings. As such, this motivates a practical framework for the design, conduct and analysis of one N-of-1 trial using existing tools for group-sequential trials.
	
	Researchers also frequently combine the results from multiple N-of-1 trials in order to estimate group-level treatment effects. In this project, we also propose how to combine the results from a series of sequentially-monitored N-of-1 trials. A key challenge is that point estimates from sequentially-monitored studies are biased, and the bias depends on each study's monitoring. To appropriately combine results, we propose first accounting for this bias by employing existing methods for de-biasing sequentially-monitored point estimates and then combining the bias-adjusted estimates with an inverse-variance weighted meta-analysis procedure. Again, this proposal allows researchers in this setting to employ existing tools and software.
	
### Sufficient Follow-Up in Studies with Long-Term Survivors
	The need to model a cure fraction, the proportion of a cohort not susceptible to the event of interest, arises in a variety of contexts including tumor relapse in oncology. A key assumption for existing methods is that subjects censored at the end of a study will not experience the event of interest. In other words, study follow-up is sufficient such that no susceptible subjects remain at the end of the study.
	
	In data examples and simulations, we find that current methods to evaluate this sufficient follow-up assumption can lead users to falsely conclude sufficient follow-up or to falsely claim insufficient follow-up. And making the appropriate decision can have important implications: for example, when planning a study with a time-to-event outcome, a cure model will frequently predict different event rates compared to a standard model.
	
	One possible reason for the undesirable behavior of existing methods could be that they are poorly calibrated for some real-world applications. Because biomedical studies necessarily end due to financial or logistical constraints, we may not reasonably expect exactly zero susceptible subjects to be remaining at the end of the study. 
	
	We have found that cure model results can be robust to some deviation from the formal condition of sufficient follow-up. This motivates us to suggest that a cure model might be appropriate with a small (but possibly non-zero) proportion of susceptible subjects remaining at the end of the study. Thus, we propose quantifying sufficient follow-up directly by studying the proportion of susceptible subjects remaining at the end of the study (or a standardized version, which we use in our method "RECeUS"). Our approach has a simpler interpretation compared to existing approaches, and, because of its general form, it accepts a flexible implementation, making it accessible to users.
	
# Future Research
	
### Platform Trials with Differing Experimental Arm Eligibility
	Our proposed extension for dynamic balancing suggests how to modify a general dynamic balancing scheme when experimental arms differ in eligibility, but we do not make a suggestion as to an "optimal" algorithm.
	
	Dynamic balancing schemes can vary in how they measure imbalance and in their weighting schemes. A weighting scheme that more preferentially assigns the new participant to the least imbalanced study arm may achieve covariate balance with fewer participants, but the treatment assignment may be more predictable for blinded investigators. An optimal algorithm would minimize predictability for a given amount of allowed imbalance and fixed sample size. 
	
	But optimality for dynamic balancing has not been well-studied in the case of more than two study arms and general weighting schemes. 
	
### Sequential Monitoring in N-of-1 Trials
	My dissertation research in this project focuses on the setting of a continuous outcome with exactly two study arms. By suggesting a mixed-effects model framework, a straightforward extension of this research is to study other types of outcomes and more than two study arms. One challenge for extending to binary and time-to-event outcomes is the limited information inherent to this setting: with short treatment periods, many observations may be censored, and we may not observe sufficient numbers of failures. 
	
	Further, in a linear mixed-effects framework, the parameter of interest can be interpreted as a marginal (across treatment blocks) treatment effect. This is particularly desirable when combining across a series of sequentially monitored N-of-1 trials. However, this interpretation does not hold for mixed-effects models without the identity link function. As such, it is important to study alternative approaches for sequential monitoring in the case of non-identity links.
	
	In addition, we assume in my dissertation that standard crossover conditions hold: without intervention, the outcome should be stable for the duration of the study and treatment effects cannot carry over into later periods. Researchers have proposed various approaches to address these assumptions if they do not hold for a particular study, but it is not well-known how these approaches perform with sequential monitoring. 
	
### Sufficient Follow-Up in Studies with Long-Term Survivors
	Parametric models are commonly used in analyzing data with long-term survivors, and my dissertation research focuses on estimation with parametric models. However, there is also a rich literature on flexible cure models, so a natural next step for this project is to employ a general class of semiparametric cure models for estimation, such as the Zeng et al.~(2006) class that includes both the proportional hazards and the proportional odds cure models as special cases. 
	
	In my dissertation, we argue that cure models may be robust to some deviation from the formal condition of sufficient follow-up based on empirical results. A long-term goal for this research is to formalize this argument and identify conditions under which the sufficient follow-up assumption can be weakened. A recent paper appearing in _Annals of Statistics_ by Patilea and Van Keilegom (2020) includes details for how a sufficient follow-up condition is used for proving consistency for their method. They also suggest that their condition may be weakened with suitable modifications to their method. As such, expanding on their results could be a promising approach for this goal.