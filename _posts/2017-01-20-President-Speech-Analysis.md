---
layout: post
title:  "State of the Union Address Text Analysis"
date:   2016-09-20
theme: cosmo
---

<p class="intro"><span class="dropcap">T</span>his post his post uses R and several text mining techniques to analyze the presidential State of the Union Address Speeches</p>


# Introduction

The State of the Union address is an (typipcally) annual speech given by the President of the United States to a joint session of Congress that outlines the President's legislative agenda, national priorities, and the current state of the country.

With the upcoming elections pending near, I thought it'd be interesting to analyze some political content. In the following post, we'll use text mining techniques to analyze the State of the Union addresses from the years 1790 to 2012. Hopefully the following analysis will showcase some of the power of text mining techniques in R.

The data used for this analysis is a very long text file containing all of the State of the Union Adress speeches from the years 1790 to 2012. It is freely available to view/download [here](http://www.gutenberg.org/ebooks/5050). 

Using the data as-is obviously won't work. However, extensive use of data cleaning (particularly regular expressions) yields a workable dataset. My code used to clean the dataset (as well as for the rest of the analysis) is available on my [github](github.com/jwilber).




In analyzing the State of the Union speeches, we can take two primary strategies: 

* analyze the speeches individually on a president-by-president basis
* analyze the speeches as an aggregate and search for general trends.

### Individual Assessment
In the individual case we can zoom in on each president and analyze them individually. For example, we can create a word cloud for each president. That said, creating a separate word cloud for all 43 presidents would be pretty difficult to analyze. Instead, as a brief example, below I juxtapose the most-common words used by Barack Obama with the most-common words used by Geroge W. Bush:

<img src="/images/bushobama_clouds.png" height="700" width="700" />


As we'd expect, multiple words are shared between the two presidents. Many of these co-occurrences are words we'd expect to see in any SOTUS speech, irrespective of the president. What makes the analysis interesting is the different words. For example, words like _terror_, _freedom_, and  _iraqi_ occur very often in Bush's speeches, revealing the pillars of policy during his time in office (particularly his focus on terrorism and the middle east). On the other hand, Obama's words, such as _job_, _economy_, and _company_ speak to the issues of his time in office, which were largely dominated by the recession.

Whiles individual analyses are undoubtedly interesting, zooming in on each  president is consuming both with regards to time and space. Thus, rather than assessing each speech individually, we'll analyze the speeches as an aggregate.


### Analyzing The Speeches In Aggregate

##### Distance Between Speeches
In order to discuss the relationship between the speeches, a distance metric must be selected. For example, a very simple distance metric for comparing speeches is the _hamming distance_. The _hamming distance_ simply measures the number of positions at which corresponding symbols are different between words. For example, the hamming distance between "_cat_" and "_can_" is 1 (to get from "_cat_" to "_can_", we must change one symbol). 

In this analysis, I utilize a much more complicated measure of distance, the Jensen-Shannon divergence. Without going into too much detail, the JS metric measures the similarity between two probability distributions, and we'll use it to measure how much one speech (or body of text) differs from another. This metric will be utilized throughout much of the following analysis.

#### Clustering Speeches

An obvious point of interest is to view which presidents share the most in common with each other. That is, which presidents, as measured by the similarity of their speeches, speak congruently. To answer this question we'll use a clustering algorithm called Hierarchical Clustering, which will create a dendrogram for easy visualization of this relationship.
In agglomerative hierarchical clustering, each observation is initialized as its own cluster, and pairs of clusters are merged going up the hierarchy until all observations fall into one class. Note that in our case, the y-axis measures the similarity of the speecehs, so the earlier in the dendrogram that observations are clustered, the more similar they are to each other. 

<img src="/images/sotus_hclust.png" height="700" width="700" />

Our dendrogram reveals, then, that Andrew Jackson and Martin Van Buren are our most similar presidents according to SOTUS content. Martin Van Buren was Jackson's Secretary of State from 1829 to 1831 and vice-president from 1833 to 1837, as well as president from 1837 to 1841, so the result is hardly surprising. 

On the other hand, John F. Kennedy appears to be the most separate from any president. While Kennedy certainly left an eneduring legacy, it is unclear why he is such an outlier (history buffs feel free to chime in). Many more observations can be made, but perhaps the most salient is that the presidents appear to be clustered in a chronological manner. For example, on the far left we can see George W. Bush alongside Bill Clinton and Barrack Obama. This pattern permeates throughout the whole of the dendrogram: Theodore Roosevelt is alongside William Howard Taft and Thomas Jefferson alongside James Madison. Notice that within these cluster, party level clustering may exist as well. For example, Obama and Clinton are clustered closer to each other than they are to Bush Jr.; Is this clustering a coincidence, or are can the speeches actually be divided up this way?

#### More Clustering≈

To investigate, we'll use two techniques in tandem: T-SNE and K-Means Clustering.

T-SNE is a relatively new dimensionality reduction technique developed by Laurens van der Maaten. More information can be found [here](https://lvdmaaten.github.io/tsne/). In this context, t-SNE should reveal any clusters in our data. Below is a plot of our t-sne embedding.

<img src="/images/uncolored_tsne.png" height="700" width="700" />


Immediately we notice that our t-SNE output appears to have some clusters in the data. In fact, the clusters are even more profound than they were for our dendrogram. But what do these clusters correspond to? If our earlier presuppositions appear to be correct; the speeches are divided into blocks based on chronological events. Judging from the names in the clusters, this appears to be the case. However, we'll investigate to find out for sure.

On top of our t-SNE plot, we'll use a basic clustering algorithm called k-means.K means is a clustering algorithm that iteratively assigns elements to clusters (based on some given distance metric) such that each cluster is as similar as possible (i.e. the variance within each cluster is as small as possible).  We'll use k-means to identify and explicitly highlight our clusters. 

<img src="/images/tsne.png" height="750" width="700" />

In this specific case, k-means performed most optimally with four clusters. I've determined the following class assignments (admittedly the names can use improvement) based on the names within those clusters.

* Cluster 1: **Early**
  * Years of Presidency: 1789 - 1901

* Cluster 2: **Pre-WW2**
  * Years of Presidency:1901 - 1933

* Cluster 3: **WW2-Viet**
  * Years of Presidency: 1933 - 1981

* Cluster 4: **Post-Viet**
  * Years of Presidency: 1981 - 2014


So clearly our data is divided into four main blocks. But why?

#### Analyzing Our Clusters

Recall that the primary aim of the SOTUS is to discuss the present state of the nation. Thus it makes sense to observe that presidents closer together in time have more similar speeches, because they're discussing similar (or related) events! Intuitively, we'd expect words like "iraq" and " terror" to be common in speeches post-2001, while absent from speeches during the 1800s. This also explains why we don't observe a large disparity among political parties; the focal point of the speeches are the nation's issues, it's the solutions to those issues that (usually) differ by party.

Now, given that we could label the presidents by name and explicitly view the results, the clusters make sense. But what if we couldn't? What if we could only go off of the information contained within each cluster? Would our results lead to the same conclusion?

Below I create four histograms, one for each timeframe. Each histogram contains the frequency of the most common words *unique* to each group. Ideally, these words will reveal the pertinent issues of each time frame.

##### Cluster 1 (Early)
<img src="/images/early_hist.png" height="700" width="700" />

Although the above plot is titled, we needn't view the title to guess which plot it is. Archaic diction, such as "prussia", "barbarian", and "hayti", saturate the plot. We can also see evidence of the Civil War and the Wild West: words like  _confederacy_, _cherokee_, and _barbarian_ no doubt hint at the early days of US history. Finally, other important issues can also be seen, such as _suffrage_.


##### Cluster 2 (Pre-WW2)

<img src="/images/ww2viet_hist.png" height="700" width="700"/>
 Given words such as _porto-rico_ and _filipino_, we can easily conclude that rhetoric deals with the Pacific. Words like _battleship_ hint at an increased navy presence. This is clearly in relation to the Phillipine-American War, which ended at the beginning of this time cluster (this period starts in 1901, the war ended in 1902). _Hague_ also reveals the time period, as the First Peace Conference at The Hague was signed in 1899, and entered into force in 1900.

##### Cluster 3 (WW2-Viet)
<img src="/images/preww2_hist.png" height="700" width="700"/>
Clearly, the above plot deals with the WW2 era, eith words like _nazi_, _tank_, and _kremlin_ jumping out immediately. In fact, he most frequently used word, _reconversion_, refers to the restoration efforts of Western Europe immediately post-World War 2. The second most popular word, _lendlea_, refers to the Lend Lease Act (1941), in which Congress authorized giving arms to to any country the President deemed vital to the defense of the United States. Moving towards Vietnam, we can see the growing importance of the Eastern Pacific with words such as _bilateral_ and _indochina_.


##### Cluster 4 (Post Viet)
<img src="/images/postviet_hist.png"  height="700" width="700"/>

Vocabulary pertaining to war and The Middle East dominate this plot, with the most salient words being _al-quada_, _hussein_, _iraq_, _saddam_, _taliban_, and the most popular of all: _terror_. The five former words can relate to either the Gulf War or post-9/11 U.S. policy. Given the high frequency of _terror_, it's likely that the majority of the rhetoric derives from post-9/11. Note, also, other important issues of the time. We can see evidence of the tech growth of the 2000's (_high-tech_, _entrepreneur_, _internet_, _math_), as well as an emphasis on jobs and education (_americorp_, _teach_, _math_). Evidence of the 90s aside from the aforementiond Middle East vocabulary is also present:  _brady-bill_, refers to the  controversial law passed in 1993 regarding background checks for handgun purchases; _bosnia_, of course, refers to the Bosnian War (1992-1995) in Bosnia and Herzegovina. Thus, were we void of a cluster title, the vocabulary would make starkingly clearly that this chunk deals with modern rhetoric.  


#### Futher Analysis
The above results, although interesting, are not surprising. After all, after discovering the four blocks in our data, it's no surprise that rhetoric would relate to issues contemporary to the blocks.

A more interesting question is assessing whether or not the groups differ in manner apart from diction.
We'll pursue this end by investigating the implicit, "meta" features of the text as opposed to the explicit vocabulary we analuzed previously. We'll investigate the following four features across the time domain of our data:

* Number of sentences used per year
* Number of words used per year
* Average word length per year
* Average sentence length per year


To make any apparent trends obvious, a regression line is fit to each of the four plots.

To make any apparent trends obvious, a regression line is fit to each of the four plots.

The results are as follows:

<img src="/images/avgsent.png" height="700" width="700"/>

Counting from left-to-right, top-to-bottom, we can see that the first three plots yield little information about general trends in the data, with the lines being more-or-less stagnant. However, the fourth plot, Average Sentence Length per Year, clearly reveals a downward slope. 

This decreasing line indicates that average sentence lengths decrease over time. Is this downward slope just a coincidence, or is this trend legitimately occuring? Analyzing the average yearly sentence length for each of the four groups (via ANOVA) determines that this result is statistically significant. 

So sentences are getting shorted over time. Why is this the case? I can think of four possible reasons for this occuring:

1. Information Compression: With the influx of information availability over the years (printer press to smart phone), information has become more and more compressed. Perhaps the plot reflects this trend, with sentences having become more concise and to the point. 

2. A linear decrease in attention spans.

3. Network pressure: A State of the Union Address can technically go on for hours. Radios/networks airing the speech may be placing pressure on the duration of the speech.

4. Stylistic Evolution (as pointed out by Katherine Chen)

While the phenomena is indeed occuring, the above three explanations are applicable only to an extent; they are weak in that they don't adequately explain why such trends exist for our earliest clusters. 

### Conclusion

Let's recap what our simple analysis has yieldeds:

- State of the Union Speeches are clustered chronologically, primarily into four groups.
- Poilitical party
- We learned the popular terms that help decide each era.
- With regard to his SOTUS rhetoric/diction, John F. Kennedy is an outlier.
- Sentences have, on average, gotten shorter over time.

Unfortunately, I am not a historian, so any commentary I can offer on our observations is quite limited. That said, I think it's very interesting the plethora of information simple statistical methods can obtain. My hope is that this post inspired you and opened your eyes to the power of statistical methods and ubiquity of of their applications.



