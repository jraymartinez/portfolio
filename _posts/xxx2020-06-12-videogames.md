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
#### Table 1. Sample Filtered Dataset
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
We transformed the dataset into a matrix of 1s and 0s. The columns of the new dataframe should represent the video games, whereas the rows represent the players. A table cell is set to 1 if a user has played the game for more than a specified number of hours; otherwise, its value is 0. Afterwards, we would likely utilize the python library MLXtend to automatically perform the apriori principle to determine the frequent itemsets. The said library could also generate association rules given these itemsets where the pattern evaluation metrics like support, confidence, and lift are listed. Based on these rules, not only can we create meaningful insights but also can provide recommendations with respect to associated or correlated video games.

### 3. Data Preprocessing
Data preprocessing was implemented on the acquired article text. The text preprocessing involves:

- Neutralizing text case-sensitivity by converting text to lowercase
- Omitting unnecessary whitespaces by removing leading and trailing whitespace
- Converting words to root form by performing stemming, via NLTK’s `PorterStemmer`.

### 4. Exploratory Data Analysis 
To see if some obvious themes or topics stand out in the article corpus, exploratory data analysis was performed on the data before clustering. [Figure 2](#fig2) shows the word cloud and word frequency graph for the Rappler news articles published from January 2018 to May 2019. Both show that **President Rodrigo Duterte is the most mentioned word in the dataset**, suggesting that Duterte is a prominent topic in Rappler's news articles from January 2018 to May 2019, and at least one article cluster should have Duterte as the recurring theme. Other notable words include government, Philippines, police, and justice. To verify these initial findings, feature extraction and cluster analysis were performed on the dataset.

## RESULTS
To determine the optimal number of clusters, k-means clustering was implemented for different values of the cluster count k from k=2 to k=20. Shown in [Figure 3](#fig3) is the variation in the values of the different internal validation measures as the cluster count k is increased. The silhouette coefficient is monotonically increasing as the number of clusters is increased, suggesting increasing separation of the clusters. However, to keep the clustering parsimonious, the SSE elbow method was used instead to determine the optimal value of k. From the graph below, the SSE graph has an elbow at around **k=10**, suggesting optimal clustering at that value.   

![Figure 3]({{ site.url }}{{ site.baseurl }}/assets/images/rappler_validation.png)
<a id="fig3"></a> 
#### Figure 3 Plots of the various internal validation measures for k=2 to k=20. The SSE graph has an elbow at k=10, suggesting optimal clustering at that value. 

### 1. Article clusters (k=10)
k-means clustering was performed on the Rappler articles using a cluster count of k=10. To infer the underlying theme of each article cluster, cluster word clouds were created as shown in [Figure 4](#fig4).

Form these word clouds, the underlying theme of each article cluster was identified as follows:

- **Cluster 1**: Legislative
- **Cluster 2**: Foreign Affairs (PH-China Relations)
- **Cluster 3**: General News
- **Cluster 4**: Judiciary
- **Cluster 5**: Weather
- **Cluster 6**: President Rodrigo Duterte
- **Cluster 7**: 2019 Philippine Midterm Elections
- **Cluster 8**: Police
- **Cluster 9**: Boracay Rehabilitation
- **Cluster 10**: Health

![Figure 4]({{ site.url }}{{ site.baseurl }}/assets/images/rappler_wordcloud.png)
<a id="fig4"></a> 
#### Figure 4 Word cloud for each article cluster (k=10). From these word clouds, the underlying theme for each article cluster were identified as follows: Cluster 1 (Legislative); Cluster 2 (Foreign Affairs); Cluster 3 (General News); Cluster 4 (Judiciary); Cluster 5 (Weather); Cluster 6 (President Rodrigo Duterte); Cluster 7 (2019 Philippine Midterm Elections); Cluster 8: (Police); Cluster 9 (Boracay Rehabilitation); Cluster 10 (Health)

Shown in [Figure 5](#fig5) is the relative size of the clusters in terms of the number of articles. Excluding the General News cluster which accounts for more than 25% of the articles, **Duterte is the largest article cluster**, comprising more than 15% of the news articles. This validates the initial results of the exploratory data analysis. 

![Figure 5]({{ site.url }}{{ site.baseurl }}/assets/images/rappler_themes_10.png) 
<a id="fig5"></a> 
#### Figure 5. Resulting article themes for k=10. The clusters are relatives balanced in terms of cluster size, except for one cluster (General News) which contains more than 25% of all articles. Excluding the General News cluster, the Duterte cluster accounts for the most number of articles. 

## INSIGHTS
The application of unsupervised clustering technique on a corpus of 11,079 news articles shows a consistency of topic clusters across different resolutions that include:

### A. Duterte article cluster
The **dominant theme of Rappler news articles is Philippine President Rodrigo Duterte**, with nearly 16% of news articles in this cluster. As seen in [Figure 6](#fig6), subthemes in this cluster include the war on drugs, human rights, Senator Antonio Trillanes, and Duterte’s ongoing war versus Rappler. This can imply that Rappler is particular with the President’s undertakings and that while this may be reasonable, Rappler has to review its focus given their strife with the President.

![Figure 6]({{ site.url }}{{ site.baseurl }}/assets/images/rappler_duterte.png) 
<a id="fig6"></a> 
#### Figure 6. Word cloud and top words for the Duterte article cluster. From the top words, it can be inferred that the subthemes of this cluster include human rights violations, the war on illegal drugs, and Senator Antonio Trillanes.

### B. Philippine Politics article cluster (Legislative and Judiciary)
The other major themes are related to the other branches of the Philippine government, particularly the **Legislative branch** (House of Representatives, Senate) and the **Judicial branch** (Supreme Court). 

Subthemes in the Judicial cluster ([Figure 7](#fig7)) are the impeachment of former Chief Justice Maria Lourdes Sereno and Leila de Lima. Impeachment of former Chief Justice Lourdes Sereno because of failure to disclose assets in her SALN, and misuse of public funds among other things. Drug charges filed by the DOJ against Senator Leila de Lima.

![Figure 7]({{ site.url }}{{ site.baseurl }}/assets/images/rappler_judiciary.png)
<a id="fig7"></a> 
#### Figure 7. Word cloud and top words for the Judiciary article cluster. From the top words, it can be inferred that the subthemes of this cluster include the impeachment of former Chief Justice Lourdes Sereno and the drug cases against Senator Leila De Lima.

Subthemes in the Legislative article cluster ([Figure 8](#fig8)) are budget Proposed changes in the constitution to shift to a federal type of government. Like the dominant clusters, this cluster focus on politics. It is apparent that Rappler is focused on the political landscape in the Philippines with a particular focus on hot and relevant issues.

![Figure 8]({{ site.url }}{{ site.baseurl }}/assets/images/rappler_legislative.png)
<a id="fig8"></a> 
#### Figure 8. Wordcloud and top words for the Legislative article cluster. From the top words, it can be inferred that the subthemes of this cluster include the national budget and the proposed shift to a federal system.

### C. Police and Weather Clusters
Two recurring themes regardless of the number of clusters selected are police reports ([Figure 9](#fig9)) and weather reports ([Figure 10](#fig10)). In line with the Duterte cluster,  it is sensible that the cluster about the police can be generated given the “oplan tokhang” implemented by the administration. Meanwhile, the weather cluster is sound considering the country’s geographic circumstances.   

![Figure 9]({{ site.url }}{{ site.baseurl }}/assets/images/rappler_pnp.png)
<a id="fig9"></a> 
#### Figure 9. (a) Wordcloud and (b) Top words in the Police article cluster

![Figure 10]({{ site.url }}{{ site.baseurl }}/assets/images/rappler_weather.png)
<a id="fig10"></a> 
#### Figure 10.  (a) Wordcloud and (b) Top words in the Weather article cluster

### D. Time-specific article clusters
The remaining themes are time-related and reflect major events during the timeframe selected (January 2019 to May 2019), such as the **2019 Philippine Midterm Elections**, **Boracay Island Rehabilitation** (April 2018-October 2018), and the **Dengvaxia (dengue vaccine) controversy**.

![Figure 11a]({{ site.url }}{{ site.baseurl }}/assets/images/rappler_current.png)
![Figure 11b]({{ site.url }}{{ site.baseurl }}/assets/images/rappler_boracay.png)
![Figure 11c]({{ site.url }}{{ site.baseurl }}/assets/images/rappler_health.png)
<a id="fig11"></a> 
#### Fig 11. Time-specific article clusters (a) 2019 Midterm Elections, (b) Boracay Rehabilitation, (c) Dengue vaccine (Dengvaxia) controversy

### E. Sensitivity Analysis
While it was concluded that 10 is the optimal number of groupings for the subject dataset, sensitivity analysis has been performed to test the robustness of the results gathered. Shown below are the resulting article clusters for k=6 ([Figure 12](#fig12)) and k=16 ([Figure 13](#fig13)). It is noted that as the cluster count is increased, the most affected clusters are bigger ones, especially the _Duterte_ cluster. As such, it can be deduced that said cluster has many subclusters which are differentiated when cluster count is increased. Nevertheless, the core clusters (e.g., General News, Duterte, 2019 Election, Police) created regardless of the number of clusters are constant. 

![Figure 12]({{ site.url }}{{ site.baseurl }}/assets/images/rappler_6.png)
<a id="fig12"></a> 
#### Figure 12. Clustering and Cluster size distribution for k=6

![Figure 13]({{ site.url }}{{ site.baseurl }}/assets/images/rappler_16.png)
<a id="fig13"></a> 
#### Figure 13. Clustering and Cluster size distribution for k=16

## SUMMARY AND CONCLUSIONS
Grouping of articles into clusters of related topics by unsupervised clustering method has  significant value to communication researchers and media practitioners in studying news output at scale and its repercussions. This study was able to _unwrap 10 major themes_ ranging from General News, Politics, Weather, Health and relevant events. As such, the result can be used as a starting point for a generalized theme extraction project from a national corpus to learn the general interest and sentiments of the people.

## RECOMMENDATIONS
The following points can be considered in future research related to this work:

- **Comparative cluster analysis with other Philippine news outfits** (Inquirer, ABS-CBN News, GMA News) can be explored to validate Rappler’s focus on particular topics;
- **Sentiment analysis can explored to look into the subjective information or emotional states of the article**. The value of combining clustering with sentiment analysis could be implemented in making better sense of Rappler’s public opinion on trending issues or the current administration; and,
- **Historical analysis can be explored to compare the Rappler data during previous administrations with the current to recognize the difference in Rappler’s focus per administration.** Administration changes can affect the political landscape and prioritization of complex issues. For instance, if an issue from one administration was solved in the next administration.

## REFERENCES
[1] <a id='ref1'></a>M. Snider, Video games can be a healthy social pastime during coronavirus pandemic, USA Today, March 29, 2020. [Online]. Available: [https://www.usatoday.com/story/tech/gaming/2020/03/28/videogames-whos-prescription-solace-during-coronaviruspandemic/2932976001/](https://www.usatoday.com/story/tech/gaming/2020/03/28/videogames-whos-prescription-solace-during-coronaviruspandemic/2932976001/). [Accessed May 7, 2020].

[2] <a id="ref2"></a>P. Bertens, A. Guitart, P. P. Chen and A. Perianez, A Machine-Learning Item Recommendation System for Video Games, 2018 IEEE Conference on Computational Intelligence and Games (CIG), Maastricht, 2018, pp. 1-4, doi: 10.1109/CIG.2018.8490456.

[3] <a id="ref3"></a>O’Neill, M., Vaziripour, E., Wu, J., Zappala, D.: Condensing steam: distilling the diversity of gamer behavior. In Proceedings of the 2016 Internet Measurement Conference, IMC 2016, pp. 81-95. ACM, New York (2016). [https://doi.org/10.1145/2987443.2987489](https://doi.org/10.1145/2987443.2987489.).

[4] <a id="ref4"></a>Tamber Team. (2017, March). Steam Video Games. Retrieved May 10, 2020 from [https://www.kaggle.com/tamber/steam-video-games/](https://www.kaggle.com/tamber/steam-video-games/).

[5] <a id="ref5"></a>D. J. Prajapati, S. Garg and N. C. Chauhan," Interesting association rule mining with consistent and inconsistent rule detection from big sales data in distributed environment, " Future Computing and Informatics Journal, pp. 1-12, 2017.