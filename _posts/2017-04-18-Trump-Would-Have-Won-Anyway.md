---
layout: post
title:  "The Electoral College Didn't Affect The 2016 Election"
date:   2015-01-17
theme: cosmo
---

# Trump Would Have Won Anyway



The USA prides itself on being a symbol of democracy, but in light of recent elections, it's electoral process,the [electoral college](), has found itself in a position of criticism. People claim that it gives a voice to states that otherwise would go ignored, while some claim it's unfair for giving Joe Smith's vote in Montana more weight than Chad Yee's in California. Others claim it's arbitrary - after all, [reforming just two state borders and shifting only four counties]() would have resulted in a Hillary Clinton victory. This post investigates the elctoral college. Specifically, it aims to answer the following question: 

	***Does the electoral college favor one party over another, and if so, did this bias affect the election outcome?***


Add: Each state gets a minimum of three electoral votes, regardless of population, which gives low-population states a disproportionate number of electors __per__ capita.[119] For example, an electoral vote represents nearly four times as many people in California as in Wyoming

***



To investigate any bias inheret in the electoral college, we'll randomize state creation in the United States of America. In this way we can simulate multiple electoral outcomes using the same data, and gain a more accurate idea of the role the elctoral college plays in our elections. 

![alt-text-1](https://github.com/jwilber/Randomized_Election/blob/master/images/randomstates.gif?raw=true "title-1" height="100" width="100") ![alt-text-2](https://github.com/jwilber/Randomized_Election/blob/master/images/randomstates_win.gif?raw=true	 "title-2" height="100" width="100")


[INSERT GIF of SHUFFLED PLOTs] side by side with voter outcome

Using the same data, our randomization scheme has yielded vastly different voting outcomes:

[VOTE BY STATE PLOT]

As you can see, the outcome changes quite often for some states.


Analysis: Cite specific state difference (CA NY) Analyze plots. Why Cali changes in size

<!-- This process can be repeated over and over again, generating new states, vote outcomes, and election winners on each iteration:

[INSERT 2x2]

Simulating this process over and over will reveal interesting trends in our data. It will DISCUSS REASON TO SIMULATE
 -->

This simulation also reveals enlightening information about the electoral college. Let's view the distribution of electoral votes per party across all 1,000 such simulations, using our current system of the electoral college:


[ELECTORAL VOTES HISTOGRAMS]
The black line signifies the majority rule. Clearly, Republicans attain more electoral votes, more often than do Democrats.

They also consistently win states.
[State Bar Plots]

In fact, as a state's population grows, so too does its propensity to end up Republican:






Talk about distributions
What's interesting is that this consistency in Republican domination exists despite Democrats having more majority votes. Discuss More
[ Insert Vote Barplot]

Other interesting trends occur as well. As the population of a state increases, so too does its propensity to vote Republican:

[insert scatter plot]

This result is unintuitive, but makes sense upon inspection. Geographically, Democrats tend to cluster in cities and coastal towns. Republicans, while mostly present in the middle of the country (the so-called 'flyover' states), are spread about the whole of the country. Thus, as a state expands, it has a higher probability of encompassing Republican counties than Democrat counties. DISCUSS PARTICULAR STATES?



Playing with the Electoral College

So how exactly does the electoral college favor Republicans? 3-vote uniform value. This isn't new information, but hopefully the above simulations reveal it's problem.
Let's observe what happens when we change the number of allotted electoral college votes
[change] analyze [change] analyze [change] analyze
Conclude
Ideally, if you live in a democracy, then regardless of your political loyalty you want a representative system. That is, you want a system where majority vote dictates rule.

People criticise the electoral college for saying that it gives unequal representation to smaller states. We removed this unequal representation and showed that no matter what the pre-apportioned amount of electoral college votes, Republicans still would have won the election. This despite there having been more Democratic votes in total. This is true both for simulated and non-simulated states.

So does the electoral college favor Republicans? In its current implementation with 3 apportioned votes per state: yes. Is this biased system responsibe for swinging the election to Republicans? No.

Finally, at this stage you may be wondering why we're not discussing the total per-party votes in the election. Our data was generated from an electoral college system election, so inferences about that can be discussed with decent accuracy.