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
Steam, the largest digital distribution platform for PC gaming, has 6000 games and a community of millions of gamers. One study shows that searchability is one of the reasons why Steam is growing so rapidly [[3](#ref3)]. Moreover, it has experienced explosive growth in 2018. This platform attracted a lot of companies to source out their data. Tamber, an analytics service company, was able to manually crawl the data from the Steam API in 2017.

As per Kaggle documentation [[4](#ref4)], the dataset which is approximately nine megabytes of data is represented into the following columns:

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
We transformed the dataset into a matrix of 1s and 0s. The columns of the new dataframe represent the video games, whereas the rows represent the players. A table cell is set to 1 if a user has played the game for more than or equal to the median number of hours played; otherwise, its value is 0 as shown in [Table 2(#table2)]. We utilized the Python library MLxtend to automatically perform the Apriori principle to determine the frequent itemsets. The library also generated association rules given these itemsets where the pattern evaluation metrics like support, confidence, and lift are listed. Based on this discretization, we generated association rules and built a recommender system.

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

The most frequent 1-itemset is Dota 2 as shown in [Table 4(#table4)]. It dominates the Steam gaming world. The results for frequent 2-itemsets and 3-itemsets in [Table 5(#table5)] and [Table 6(#table6)] respectively are not necessarily interesting since it is quite expected that popular games such as Dota 2 and Team Fortress 2 would co-occur more than others. Hence, we did some research on relative co-occurrence analysis and found a metric called all-confidence [[5](#ref5)], which is equal to the equation 1 below.

                   all-confidence(X⇒Y) =  support(X⇒Y) / max(support(X), support(Y))       (1)

If the all-confidence is equal to 1, then itemsets X and Y always co-occur relatively. This is equivalent to saying that both confidence(X⇒Y) and confidence(Y⇒X) are equal to 1.

Since MLxtend does not compute the all-confidence metric, we implemented a function and found the following frequent 2-itemsets.



## RESULTS

As observed, the popular game Dota 2 is nowhere to be found in the Top 5. This is because the frequency of 2-itemsets has been computed on a relative basis (all-confidence).

<a id="table7"></a> 
#### Table 7. Top 5 Frequent 2-itemsets (Based on All-Confidence).
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

Speaking of all-confidence, this metric seems to be reliable enough for co-occurrence analysis since the results above are quite sensible. For instance, Half-Life 2 Episode One and Half-Life 2 Episode Two are shown to co-occur frequently despite not being popular as shown in [Table 7(#table7)]. Looking at their titles, one is probably a sequel of the other. This means that players are highly interested in completing the game series since the co-occurrence is relatively high.In addition, Call of Duty Modern Warfare 3 and Call of Duty Modern Warfare 3 - Multiplayer appear to co-occur frequently as well. This makes sense since these games are actually related to each other content-wise, not to mention how similar their game titles are. The key difference of these two is that the former has a single-player mechanics while the latter is multiplayer-oriented which requires interaction with other players. Hence, it seems that many of those who played the single player campaign also wanted to try the multiplayer mode, and vice-versa.

To avoid the limitation of the support-confidence framework (i.e., high support and high confidence could happen by chance), we primarily use the evaluation metric 'lift' to find more meaningful associations. The idea is to provide recommendations based on strongly correlated video games.

Sorted based on highest 'lift', the generated rules are consistent with our results earlier. Half-Life 2 Episode One and Half-Life 2 Episode Two are part of the top list. Having a huge lift of 65.07, these two games indeed have strong, positive correlation. Moreover, it is expected that Call of Duty Modern Warfare 3 and Call of Duty Modern Warfare 3 - Multiplayer are also strongly correlated with a lift of 41.47.

<a id="table8"></a> 
#### Table 8. Sample of Interesting Rules.
<table>
<thead>
<tr>
<th>A</th>
<th>B</th>
<th>A Support</th>
<th>B Support</th>
<th>support(A⇒B)</th>
<th>confidence(A⇒B)</th>
<th>lift</th>
<th>leverage</th>
<th>conviction</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>(The Elder Scrolls V Skyrim)</code></td>
<td>(Fallout 4)</td>
<td>0.047315</td>
<td>0.011794</td>
<td>0.005273</td>
<td>0.111437</td>
<td>9.448542</td>
<td>0.004715</td>
<td>1.112139</td>
</tr>
<tr>
<td><code>(The Elder Scrolls V Skyrim)</code></td>
<td>(BioShock Infinite)</td>
<td>0.047315</td>
<td>0.014847</td>
<td>0.006244</td>
<td>0.131965</td>
<td>8.888508</td>
<td>0.005541</td>
<td>1.134923</td>
</tr>
</tbody>
</table>

One of the interesting rules that we find cool enough is that The Elder Scrolls V Skyrim and Fallout 4 are highly correlated with a lift of 9.45 as shown in [Table 8(#table8)]. Amazingly, we have found out that bundles of these two games are currently being sold not only on Steam but also on the PlayStation Store. It seems that Steam and PlayStation are aware that players frequently played these two games together before, and that's why these games are recently being sold as a bundle for both [PC](https://store.steampowered.com/bundle/6527/Skyrim_Special_Edition__Fallout_4_GOTY/) and [PS4](https://store.playstation.com/en-us/product/UP1003-CUSA02557_00-FO4GOTYSSEBUNDLE) console gaming. 

From the same table, another interesting rule indicates that The Elder Scrolls V Skyrim and BioShock Infinite are also highly correlated with a lift of 8.89. We have found out that a bundle of these two games, for PlayStation 3 this time, are actually being sold on [Amazon.com](https://www.amazon.com/Elder-Scrolls-Skyrim-Bioshock-Infinite-PlayStation/dp/B00HV0MNEI). Again, this means that these two games might really have a strong association and that's why they're being sold as part of a bundle.

## DISCUSSION AND FUTURE WORKS
In this study, after trying multiple thresholds, we learned that the threshold of 0.5% provides acceptable interpretability of results. We use this support threshold to consider a set of frequent video games played. It means a game set is deemed to be frequent if this set is observed in at least 0.5% of the data set of video games. Please note that the a frequent set should have at least one game while the number of games in the set cannot exceed three.

The result of the adopted approach can be summarized as follows. We show that Dota 2 is the most frequent played game. Although not as frequent as Dota 2, Team Fortress 2 is the second game observed. However, the impacts of co-occurrences of these two games are observed in frequent 2-itemsets and 3-itemsets results. Considering this observation that the popular games will always co-occur more than the others, we adopt a good strategy to perform other interesting measure 'all confidence'. As a result, popular games are not in the top games co-occurrences and the most common pair of co-occurring games is composed of Half-Life 2 Episode One and Half-Life 2 Episode Two which are obviously associated to each other being a prequel-sequel pair.

Furthermore, we focused on the video games co-occurrence analysis in a data set to come up with video games recommendation system. With the help of library MLxtend, we built the system that primarily use the built-in interesting measure 'lift' to recommend associated games. This system is able to identify meaningful associations from our co-occurrence analysis and provide games recommendations to the user. Interestingly, some of its association rules found are exactly the same game pairs sold as a bundle for both PC and PS4 console gaming. However, we are dealing with a huge number of games which is potential for large number of null transactions and the built-in interesting measure 'lift' is a not null-invariant measure. This means that 'lift' can be easily affected by null transactions giving a chance for the system to provide the user with a bad recommendation. 

With this, in the next study, we are going to focus on tasks of comparing different null-invariant measures such as 'all confidence', 'Kulczynski', etc. Since there is no such readily-made functions or modules that implement those measures, we need to create ones and integrate to the recommendation system. It will be interesting to see the the impacts of null-invariant measures along with not null-invariant to the association rules. 

Moreover, another avenue of future research that we would like to explore is the predictive power of individual and co-occurring frequent video games for the category of games. This idea is based on this fact that some of the video games are frequent in a specific category of games.

## REFERENCES
[1] <a id='ref1'></a>M. Snider, Video games can be a healthy social pastime during coronavirus pandemic, USA Today, March 29, 2020. [Online]. Available: [https://www.usatoday.com/story/tech/gaming/2020/03/28/videogames-whos-prescription-solace-during-coronaviruspandemic/2932976001/](https://www.usatoday.com/story/tech/gaming/2020/03/28/videogames-whos-prescription-solace-during-coronaviruspandemic/2932976001/). [Accessed May 7, 2020].

[2] <a id="ref2"></a>P. Bertens, A. Guitart, P. P. Chen and A. Perianez, A Machine-Learning Item Recommendation System for Video Games, 2018 IEEE Conference on Computational Intelligence and Games (CIG), Maastricht, 2018, pp. 1-4, doi: 10.1109/CIG.2018.8490456.

[3] <a id="ref3"></a>O’Neill, M., Vaziripour, E., Wu, J., Zappala, D.: Condensing steam: distilling the diversity of gamer behavior. In Proceedings of the 2016 Internet Measurement Conference, IMC 2016, pp. 81-95. ACM, New York (2016). [https://doi.org/10.1145/2987443.2987489](https://doi.org/10.1145/2987443.2987489.).

[4] <a id="ref4"></a>Tamber Team. (2017, March). Steam Video Games. Retrieved May 10, 2020 from [https://www.kaggle.com/tamber/steam-video-games/](https://www.kaggle.com/tamber/steam-video-games/).

[5] <a id="ref5"></a>D. J. Prajapati, S. Garg and N. C. Chauhan," Interesting association rule mining with consistent and inconsistent rule detection from big sales data in distributed environment, " Future Computing and Informatics Journal, pp. 1-12, 2017.