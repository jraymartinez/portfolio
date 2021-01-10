---
layout: single
header:
  teaser: /assets/images/dota2.png
  image: /assets/images/gamestop.png
  caption: "Photo credit: [**www.gamestop.com**](https://www.gamestop.com/)"
title: "Identifying Co-occurrence Based on Hours Played for Video Games"
date:   2020-06-12 16:50:00 +0800
categories: projects
mathjax: "true"
linkedin: "true"
tags: [recommender system, video games, association rules]
excerpt: "In this project, we create a game-based recommender system using association rules mining with respect to the video games that were frequently played together."
---

## AUTHORS
[John Ray Martinez](https://jraymartinez.github.io/) (jbm332@drexel.edu), [Jonathan Musni](https://www.linkedin.com/in/jonathan-musni-624773134/) (jem472@drexel.edu), [Marvin Joseph Occeno](https://www.linkedin.com/in/marvin-joseph-occeno-8b4a95120/) (mr048@drexel.edu)

<sub> *This research is implemented in fulfillment of the requirements for the Data Mining Course of Master of Science in Data Science under Drexel University College of Computing & Informatics* </sub>


## INTRODUCTION
Playing video games has always been a popular leisure activity. Recently, in light of the pandemic, people are actually encouraged to play such video games to ensure that they do stay at home [[1](#ref1)]. To let gamers keep on playing more, recommendation engines are being utilized by several online video game stores. Players receive various game suggestions which are usually based on, but not limited to, their gaming history [[2](#ref2)]. In this project, we create a game-based recommender system using association rules mining with respect to the video games that were frequently played together. The objectives of this study are to: i) identify the most played video games; ii) identify the frequent co-occurring video games; and iii) provide recommendations based on correlated video games.

## DATA DESCRIPTION
Steam, the largest digital distribution platform for PC gaming, has 6000 games and a community of millions of gamers. One study shows that searchability is one of the reasons why Steam is growing so rapidly [[3](#ref3)]. Moreover, it has experienced explosive growth in 2018. This platform attracted a lot of companies to source out their data. Tamber, an analytics service company, was able to manually crawl the data from the Steam API three years ago.

As per Kaggle documentation, the dataset which is approximately nine megabytes of data is represented into the following columns [[4](#ref4)]:

<a id="table1"></a> 
#### Table 1. Sample Filtered Dataset.
<table>
<thead>
<tr>
<th>User Id</th>
<th>Games Played</th>
<th>Number of Hours Played</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>298950</code></td>
<td>ARK Survival Evolved</td>
<td>41.0</td>
</tr>
<tr>
<td><code>76767</code></td>
<td>Call of Duty Modern Warfare 2</td>
<td>65.0</td>
</tr>
<tr>
<td><code>76767</code></td>
<td>Banished</td>
<td>24.0</td>
</tr>
<tr>
<td><code>229911</code></td>
<td>Call of Duty Modern Warfare 2</td>
<td>44.0</td>
</tr>
<tr>
<td><code>86540</code></td>
<td>Audiosurf</td>
<td>57.0</td>
</tr>
</tbody>
</table>


## METHODOLOGY
We transformed the dataset into a matrix of 1s and 0s. The columns of the new dataframe represent the video games, whereas the rows represent the players. A table cell is set to 1 if a user has played the game for more than or equal to the median number of hours played; otherwise, its value is 0. We utilized the python library MLXtend to automatically perform the Apriori principle to determine the frequent itemsets. The library also generated association rules given these itemsets where the pattern evaluation metrics like support, confidence, and lift are listed. Based on this discretization, we generated association rules and built a recommender system.

<a id="table2"></a> 
#### Table 2. Sample Transformed Dataset.
<table>
<thead>
<tr>
<th>User Id</th>
<th>ARK Survival Evolved</th>
<th>Audiosurf</th>
<th>Banished</th>
<th>BioShock Infinite</th>
<th>Borderlands 2</th>
<th>Call of Duty Black Ops</th>
<th>Call of Duty Modern Warfare 2</th>
<th>Call of Duty Modern Warfare 2 - Multiplayer</th>
<th>Call of Duty World at War</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>5250</code></td>
<td>0.0</td>
<td>0.0</td>
<td>0.0</td>
<td>0.0</td>
<td>0.0</td>
<td>0.0</td>
<td>0.0</td>
<td>0.0</td>
<td>0.0</td>
</tr>
<tr>
<td><code>76767</code></td>
<td>0.0</td>
<td>0.0</td>
<td>1.0</td>
<td>0.0</td>
<td>0.0</td>
<td>1.0</td>
<td>1.0</td>
<td>1.0</td>
<td>1.0</td>
</tr>
<tr>
<td><code>86540</code></td>
<td>0.0</td>
<td>1.0</td>
<td>0.0</td>
<td>0.0</td>
<td>0.0</td>
<td>0.0</td>
<td>0.0</td>
<td>0.0</td>
<td>0.0</td>
</tr>
<tr>
<td><code>229911</code></td>
<td>0.0</td>
<td>0.0</td>
<td>0.0</td>
<td>0.0</td>
<td>0.0</td>
<td>0.0</td>
<td>1.0</td>
<td>1.0</td>
<td>0.0</td>
</tr>
<tr>
<td><code>298950</code></td>
<td>1.0</td>
<td>0.0</td>
<td>0.0</td>
<td>1.0</td>
<td>1.0</td>
<td>0.0</td>
<td>0.0</td>
<td>0.0</td>
<td>0.0</td>
</tr>
</tbody>
</table>

### Quantitative Association Rules
Here comes the fun part - finding association rules. The first step is to determine frequent itemsets. Since the data is relatively large, we have decided to set the minimum support to 0.005. 

<a id="table3"></a> 
#### Table 3. Itemsets with minimum support of 0.005. 
<table>
<thead>
<tr>
<th>support</th>
<th>itemsets</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>0.006799</code></td>
<td>(7 Days to Die)</td>
</tr>
<tr>
<td><code>0.009713</code></td>
<td>(APB Reloaded)</td>
</tr>
<tr>
<td><code>0.010962</code></td>
<td>(ARK Survival Evolved)</td>
</tr>
<tr>
<td><code>0.009852</code></td>
<td>(AdVenture Capitalist)</td>
</tr>
<tr>
<td><code>0.014153</code></td>
<td>(Age of Empires II HD Edition)</td>
</tr>
<tr>
<td><code>     ...</code></td>
<td>     ...</td>
</tr>
<tr>
<td><code>0.006660</code></td>
<td>(Left 4 Dead 2, The Elder Scrolls V Skyrim, Te...</td>
</tr>
<tr>
<td><code>0.006244</code></td>
<td>(Unturned, Left 4 Dead 2, Team Fortress 2)</td>
</tr>
<tr>
<td><code>0.007354</code></td>
<td>(Unturned, Robocraft, Team Fortress 2)</td>
</tr>
<tr>
<td><code>0.005828</code></td>
<td>(Unturned, Terraria, Team Fortress 2)</td>
</tr>
<tr>
<td><code>0.006244</code></td>
<td>(Team Fortress 2, Unturned, Garry's Mod, Count...</td>
</tr>
</tbody>
</table>

Based on the 454 itemsets that passed the minimum support (0.005), we determined the most frequent k-itemsets below.

<a id="table4"></a> 
#### Table 4. Top 5 Frequent 1-itemsets.
<table>
<thead>
<tr>
<th>Itemset</th>
<th>Support</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>Dota 2</code></td>
<td>0.3368</td>
</tr>
<tr>
<td><code>Team Fortress 2</code></td>
<td>0.1618</td>
</tr>
<tr>
<td><code>Counter-Strike Global Offensive</code></td>
<td>0.0956</td>
</tr>
<tr>
<td><code>Unturned</code></td>
<td>0.0744</td>
</tr>
<tr>
<td><code>Left 4 Dead 2</code></td>
<td>0.0561</td>
</tr>
</tbody>
</table>

<a id="table5"></a> 
#### Table 5. Top 5 Frequent 2-itemsets.
<table>
<thead>
<tr>
<th>Itemset</th>
<th>Support</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>Dota 2, Team Fortress 2</code></td>
<td>0.0336</td>
</tr>
<tr>
<td><code>Counter-Strike Global Offensive, Dota 2</code></td>
<td>0.0319</td>
</tr>
<tr>
<td><code>Counter-Strike Global Offensive, Team Fortress 2</code></td>
<td>0.0309</td>
</tr>
<tr>
<td><code>Team Fortress 2, Unturned</code></td>
<td>0.0279</td>
</tr>
<tr>
<td><code>Left 4 Dead 2, Team Fortress 2</code></td>
<td>0.0272</td>
</tr>
</tbody>
</table>

<a id="table6"></a> 
#### Table 6. Top 5 Frequent 3-itemsets.
<table>
<thead>
<tr>
<th>Itemset</th>
<th>Support</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>Counter-Strike Global Offensive, Dota 2, Team Fortress 2</code></td>
<td>0.0132</td>
</tr>
<tr>
<td><code>Counter-Strike Global Offensive, Garry's Mod, Team Fortress 2</code></td>
<td>0.0115</td>
</tr>
<tr>
<td><code>Counter-Strike Global Offensive, Team Fortress 2, Unturned</code></td>
<td>0.0115</td>
</tr>
<tr>
<td><code>Garry's Mod, Team Fortress 2, Unturned</code></td>
<td>0.0115</td>
</tr>
<tr>
<td><code>Counter-Strike Global Offensive, Left 4 Dead 2, Team Fortress 2 	</code></td>
<td>0.0115</td>
</tr>
</tbody>
</table>

The most frequent 1-itemset is Dota 2. It dominates the Steam gaming world. The results for frequent 2-itemsets and 3-itemsets are not necessarily interesting since it is quite expected that popular games such as Dota 2 and Team Fortress 2 would co-occur more than others. Hence, we did some research on relative co-occurrence analysis and found a metric called all-confidence, which is equal to the following [[5](#ref5)]:

$$ all-confidence (X⇒Y) =  \frac{support(X⇒Y)}{max(support(X), support(Y))} $$

If the all-confidence is equal to 1, then itemsets X and Y always co-occur relatively. This is equivalent to saying that both confidence(X⇒Y) and confidence(Y⇒X) are equal to 1.

Since mlxtend does not compute the all-confidence metric, we implemented a function and found the following frequent 2-itemsets.

<a id="table7"></a> 
#### Table 7. Top 5 Frequent 2-itemsets (Based on All-Condidence).
<table>
<thead>
<tr>
<th>Itemset</th>
<th>All-Confidence</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>Half-Life 2 Episode One, Half-Life 2 Episode Two</code></td>
<td>0.6410</td>
</tr>
<tr>
<td><code>Call of Duty Modern Warfare 3, Call of Duty Modern Warfare 3 - Multiplayer</code></td>
<td>0.5755</td>
</tr>
<tr>
<td><code>Call of Duty Modern Warfare 2, Call of Duty Modern Warfare 2 - Multiplayer 	</code></td>
<td>0.5436</td>
</tr>
<tr>
<td><code>Call of Duty Black Ops, Call of Duty Black Ops - Multiplayer</code></td>
<td>0.4912</td>
</tr>
<tr>
<td><code>Total War ROME II - Emperor Edition, Total War SHOGUN 2</code></td>
<td>0.4444</td>
</tr>
</tbody>
</table>

As observed, the popular game Dota 2 is nowhere to be found in the Top 5. This is because the frequency of 2-itemsets has been computed on a relative basis (all-confidence).

Speaking of all-confidence, this metric seems to be reliable enough for co-occurrence analysis since the above results are quite sensible. For instance, Half-Life 2 Episode One and Half-Life 2 Episode Two are shown to co-occur frequently despite not being popular. Looking at their titles, one is probably a sequel of the other. This means that players are highly interested in completing the game series since the co-occurrence is relatively high.

In addition, Call of Duty Modern Warfare 3 and Call of Duty Modern Warfare 3 - Multiplayer appear to co-occur frequently as well. This makes sense since these games are actually related to each other content-wise, not to mention how similar their game titles are. The key difference of these two is that the former has a single-player mechanics while the latter is multiplayer-oriented which requires interaction with other players. Hence, it seems that many of those who played the single player campaign also wanted to try the multiplayer mode, and vice-versa.

To avoid the limitation of the support-confidence framework (i.e., high support and high confidence could happen by chance), we primarily use the evaluation metric 'lift' to find more meaningful associations. The idea is to provide recommendations based on strongly correlated video games.



## RESULTS

## SUMMARY AND CONCLUSIONS

## RECOMMENDATIONS

## REFERENCES
[1] <a id='ref1'></a>M. Snider, Video games can be a healthy social pastime during coronavirus pandemic, USA Today, March 29, 2020. [Online]. Available: [https://www.usatoday.com/story/tech/gaming/2020/03/28/videogames-whos-prescription-solace-during-coronaviruspandemic/2932976001/](https://www.usatoday.com/story/tech/gaming/2020/03/28/videogames-whos-prescription-solace-during-coronaviruspandemic/2932976001/). [Accessed May 7, 2020].

[2] <a id="ref2"></a>P. Bertens, A. Guitart, P. P. Chen and A. Perianez, A Machine-Learning Item Recommendation System for Video Games, 2018 IEEE Conference on Computational Intelligence and Games (CIG), Maastricht, 2018, pp. 1-4, doi: 10.1109/CIG.2018.8490456.

[3] <a id="ref3"></a>O’Neill, M., Vaziripour, E., Wu, J., Zappala, D.: Condensing steam: distilling the diversity of gamer behavior. In Proceedings of the 2016 Internet Measurement Conference, IMC 2016, pp. 81-95. ACM, New York (2016). [https://doi.org/10.1145/2987443.2987489](https://doi.org/10.1145/2987443.2987489.).

[4] <a id="ref4"></a>Tamber Team. (2017, March). Steam Video Games. Retrieved May 10, 2020 from [https://www.kaggle.com/tamber/steam-video-games/](https://www.kaggle.com/tamber/steam-video-games/).

[5] <a id="ref5"></a>D. J. Prajapati, S. Garg and N. C. Chauhan," Interesting association rule mining with consistent and inconsistent rule detection from big sales data in distributed environment, " Future Computing and Informatics Journal, pp. 1-12, 2017.