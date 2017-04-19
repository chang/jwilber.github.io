---
layout: post
title:  "The Electoral College Didn't Affect The 2016 Election"
date:   2015-01-17
theme: cosmo
---

# Trump Would Have Won Anyway



The United States of America prides itself on being the world symbol of democracy; a place where eve ..., However in light of recent elections, it's election process,the [electoral college](), has found itself in a position of criticism. 


On the one hand, some people claim that it's necessary and gives a voice to states that otherwise would go ignored, while some claim that it's unfair for giving a disproportionate amount of votes to low-population states. Others claim it's arbitrary - after all, [reforming just two state borders and shifting only four counties]() would have resulted in a Hillary Clinton victory. 



This post investigates the elctoral college. Specifically, it aims to answer the following question: 

***Does the electoral college favor one party over another, and if so, did this bias affect the election outcome?***

***

### Randomizing the Election

To investigate any bias inheret in the electoral college, we'll randomize state creation in the United States of America. 

![Random State Constructions](https://github.com/jwilber/Randomized_Election/blob/master/images/randomstates2.gif?raw=true "title-1")

In this way we can simulate multiple electoral outcomes using the same data, and gain a more accurate idea of the role the elctoral college plays in our elections.

 ![Random States Color-coded by Victory](https://github.com/jwilber/Randomized_Election/blob/master/images/randomstateswins2.gif?raw=true	 "title-2")

We can see multiple examples of state outcomes changing due to the counties they encompass. For example, when we view the vote distribution per state, we can see quite a lot of differences:


Examples abound of state-level election outcome changing as a function of a state's county composition. For example, we can see that the so-called Democratic '*Costal Elite Party*' stereotype usually holds true - states touching the West Coast overwhelmingly turn blue. However, look at Nevada in the above sample of simulations; as state size ventures too far inward, the vast number of Republican counties overtakes the Democrat majority, and the state ends up voting Red. 

![Votes by State](https://github.com/jwilber/Randomized_Election/blob/master/images/votes_per_state2.gif?raw=true "title-1")


 When looking at eah states vote count per party, we see a lot of variance. Regardless of the implications this variance has on the arbitrariness of state boundaries, what's interesting is that the same geographic trends seem to emerge: The Democrats (the so-called:) hold the coast, while the Republicans (the so-called:) hold the central sea-of-red.

***


### The Electoral College

Under the current scheme, each state is assigned a minimum of 3 electoral votes, leaving 385 remaining votes to be assigned based on state population.

This process of pre-apportioning votes is often criticised for giving low-population states a disproportionate number of electors per capita (e.g., an electoral vote represents nearly four times as many people in California as in Wyoming). However, concensus on the bias inherent in the electoral college is still a topic of much dispute.

Recall, the electoral vote distribution for the 2016 election was as follows:

| Party      | # Electoral Votes |
|------------|-------------------|
| Democrat   | 232               |
| Republican | 306               |



Using the above randomization scheme, we can produce multiple election outcomes and view the distribution of obtained electoral votes per party. In this way, we can get better visualize the distribution of possible election outcomes, as well as measure the likelihood of obtaining the results we did.

First, we can view the number of states won by each party across the simulations.

Republicans clearly win much more states than Democrats. In fact, in every randomization, Repbulicans win more states than Democrats. This result isn't surprisng, it's actually expected:


![Votes by State](https://github.com/jwilber/Randomized_Election/blob/master/images/scatterplots.gif?raw=true "title-1")

While it's true that Democratic counties tend to have much higher populations, the United States has far more Republican counties than Democrat counties. Thus, during randomization the probability of a state absorbing a red county (and therefore a red population) is far more likely on average than a blue county. 


 This difference in state victories isn't necessarily important. In America's winner-take-all election process, what really matters is the number of electoral votes each state brings.

![Votes by State](https://github.com/jwilber/Randomized_Election/blob/master/images/hist_ev_1.png?raw=true "title-1")


In this case, Repbulicans *are* accrueing more electoral votes than Democrats. What's more, they're doing so more often.

All of this, of course, culminates into more election victories for Republicans:

![Votes by State](https://github.com/jwilber/Randomized_Election/blob/master/images/total_elec1.png?raw=true "title-1")

So clearly Republicans attain much more victories than do Democrats, despite the Democrats having a majority total vote amount. Is this result because the electoral college in its current form is biased towards Republicans? Or would the outcome be the same regardless of pre-apportionment?



### Investigating Bias in the Electoral College








[ELECTORAL VOTES HISTOGRAMS]
The black line signifies the majority rule. Clearly, Republicans attain more electoral votes, more often than do Democrats.

They also consistently win more states.
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