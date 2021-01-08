---
layout: single
header:
  teaser: /assets/images/wordcloud.png
  image: /assets/images/mariaressa20190206.jpg
  caption: "Photo credit: [**Reporters Without Borders**](https://rsf.org/)"  
title: "unwRAPPLER: Identifying Underlying Themes in Rappler News Articles"
date:   2019-07-23 16:50:00 +0800
categories: projects
mathjax: "true"
excerpt: "This study aims to uncover the underlying themes of Rappler news articles via unsupervised clustering techniques and see if there is an inherent concentration of news in a specific theme."
tags: [natural language processing, unsupervised learning, clustering, theme extraction, Rappler, data mining]
---

## AUTHORS
[Carmelita Esclanda](https://www.linkedin.com/in/carmelita-esclanda-566b2946/) (cesclanda@aim.edu), [George Allan Esleta](https://gpsleta.github.io/) (gesleta@aim.edu), Elmer Robles (erobles@aim.edu), Sandro Luis Silva (ssilva@aim.edu)

## EXECUTIVE SUMMARY
Rappler, one of the leading online news publishers in the Philippines, seeks to inspire community engagement and create action for social change through citizen journalism. However, it has recently been under scrutiny by the Philippine government for “twisted” reporting. This study aims to uncover the underlying themes of Rappler news articles via unsupervised clustering techniques and see if there is an inherent concentration of news in a specific theme. A total of 11,079 articles were extracted from Rappler’s national news section published from January 2018 to May 2019. Features were extracted from the articles using a term frequency-inverse document frequency (TF-IDF) vectorizer and dimensions were reduced by implementing Latent Semantic Analysis (LSA). Lastly, unsupervised clustering via k-means algorithm was applied to group the articles and internal validation metrics were utilized to determine the optimal number of clusters. Ten clusters were uncovered, with Philippine President Rodrigo Duterte as the dominant cluster. The remaining themes touch on different branches of government, police and weather updates, and trending national issues. The insights gained from this research can aid Rappler in balancing its reporting by lessening bias towards specific topics.

![poster]({{ site.url }}{{ site.baseurl }}/assets/images/rappler_poster.png)

## INTRODUCTION
Rappler is one of the leading online news publishers in the Philippines. It was started in 2011 by former CNN journalist Maria Ressa. However, since 2018, Rappler has been under heavy scrutiny by the Philippine government for “twisted” and “biased reporting” [[1](#ref1)].  Philippine President Rodrigo Duterte even went so far as calling Rappler a “fake news” outlet that publishes articles that are “pregnant with falsity” [[2](#ref2)]. Rappler has been on the receiving end of criminal cases from the Philippine governments. BIR filed several counts of tax evasion charges against Rappler CEO Maria Ressa. Cyber-libel cases were also filed against Ressa.

Why is Rappler being targeted by the Duterte Administration? Is Rappler “twisted” and “biased” in its reporting? In this work, we uncovered the underlying themes of Rappler’s news articles via unsupervised clustering, to see if there is indeed an inherent concentration of news in a specific topic or theme.

## BUSINESS VALUE
Extracting themes from a set of articles programmatically has a widespread application in the digital publishing industry and can be used to deliver business value to readers, journalists, advertisers, aggregators, and researchers.  

- **Readers** in the digital age have no patience. They are more likely to use a search engine to retrieve a set of ranked articles from multiple news sources and it becomes a challenge for online news platforms to engage a reader continuously. Automatic theme extraction and clustering of articles provide the ability to structure a set of articles to make it easier for readers to navigate to related articles. If articles can be presented in a logical hierarchy driven by patterns in the data, human intervention is minimized (saving on labor costs) and the reader is kept on the news platform, increasing engagement time on the site.

- **News Publishers and Journalists** seeking to address topics of broad interest to their readership can benefit from a thematic clustering of articles to determine the balance of news coverage. Publishing organizations are always looking for gaps in news coverage to offer readers some perspective and insight into topics that are not heavily covered. By examining existing themes holistically, they can better gauge what is missing and what their next article should be about. 

- **Advertisers** that are considering online news platforms to reach specific customer segments can tailor their messages so that they are congruent with the themes that readers are interested in. For instance, themes dealing with legislative or judicial proceedings may appeal to advertisers whose clients are lawyers or law schools.  Advertisers of tourism and tourist agencies may be interested in weather and specific vacation destinations, such as Boracay. 

- **Aggregators** in the licensed publishing industry create packages of content for redistribution. Their business model, which can be subscription or advertiser-based, is to target specific customers based on their geographic, demographic, and psychographic profile. For instance, if an investor wanted to understand market conditions for a particular industry, they would subscribe to a real-time news delivery service that was able to provide the relevant articles.

- **Researchers** make money by selling analytical reports. By studying the themes presented on news platforms and combining the study with other metrics such as readership engagement, sentiment analysis, and political stance, they can make in-depth comparisons with other news delivery platforms to better inform advertisers and aggregators.

## METHODOLOGY
To uncover the underlying themes, a total of **11,079 news articles** published from **January 2018 to May 2019** were retrieved from Rappler's Nation section (`https://www.rappler.com/nation`). The general workflow for clustering the Rappler articles as shown in [Figure 1](#fig1) involves the following steps:

1. Data Extraction
2. Data Storage
3. Data Preprocessing
4. Exploratory Data Analysis
4. Feature Extraction via TFIDF Vectorization
5. Dimensionality Reduction using Latent Semantic Analysis (LSA)
6. Unsupervised clustering using *k*-means algorithm

Each step of the workflow will be discussed in the succeeding sections. 

![Figure 1]({{ site.url }}{{ site.baseurl }}/assets/images/rappler_methodology.png)
<a id="fig1"></a> 
#### Figure 1. Workflow for clustering the Rappler articles 

### 1. Data Extraction
News articles published from January 2018 to May 2019 were extracted from the [Rappler's Nation section](https://www.rappler.com/nation) via web scraping tools, specifically Python’s `requests` and `BeautifulSoup` modules. The process involved extracting the article text and selected metadata. Initial cleaning was also implemented to remove image captions, author and photographer details, location headers, hyperlinks, social media texts, and general sign-offs.

### 2. Data Storage
The extracted articles were stored in a local `sqlite` database. A total of 11,079 news articles were stored in the database. [Table 1](#table1) shows the data description:

<a id="table1"></a> 
#### Table 1. Data dictionary
<table>
<thead>
<tr>
<th>Data</th>
<th>Data type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>article_id</code></td>
<td>VARCHAR</td>
<td>Unique ID identifier</td>
</tr>
<tr>
<td><code>url</code></td>
<td>VARCHAR</td>
<td>Relative URL</td>
</tr>
<tr>
<td><code>headline</code></td>
<td>VARCHAR</td>
<td>Headline title</td>
</tr>
<tr>
<td><code>metadesc</code></td>
<td>VARCHAR</td>
<td>Quick synopsis of the article</td>
</tr>
<tr>
<td><code>label</code></td>
<td>VARCHAR</td>
<td>Absolute URL</td>
</tr>
<tr>
<td><code>author</code></td>
<td>VARCHAR</td>
<td>Author name(s)</td>
</tr>
<tr>
<td><code>published_date</code></td>
<td>VARCHAR</td>
<td>Published date</td>
</tr>
<tr>
<td><code>updated_date</code></td>
<td>VARCHAR</td>
<td>Date updated</td>
</tr>
<tr>
<td><code>article</code></td>
<td>VARCHAR</td>
<td>Article text</td>
</tr>
<tr>
<td><code>metakey</code></td>
<td>VARCHAR</td>
<td>List of metatags associated with the article</td>
</tr>
</tbody>
</table>


### 3. Data Preprocessing
Data preprocessing was implemented on the acquired article text. The text preprocessing involves:

- Neutralizing text case-sensitivity by converting text to lowercase
- Omitting unnecessary whitespaces by removing leading and trailing whitespace
- Converting words to root form by performing stemming, via NLTK’s `PorterStemmer`.

### 4. Exploratory Data Analysis 
To see if some obvious themes or topics stand out in the article corpus, exploratory data analysis was performed on the data before clustering. [Figure 2](#fig2) shows the word cloud and word frequency graph for the Rappler news articles published from January 2018 to May 2019. Both show that **President Rodrigo Duterte is the most mentioned word in the dataset**, suggesting that Duterte is a prominent topic in Rappler's news articles from January 2018 to May 2019, and at least one article cluster should have Duterte as the recurring theme. Other notable words include government, Philippines, police, and justice. To verify these initial findings, feature extraction and cluster analysis were performed on the dataset.

![Figure 2]({{ site.url }}{{ site.baseurl }}/assets/images/rappler_eda.png)
<a id="fig2"></a> 
#### Figure 2. Exploratory analysis of Rappler news articles published from January 2018 to May 2019 (a) word cloud of the Rappler news articles (b) word count of the 15 most occurring words in the Rappler article corpus. Both the word cloud and the word frequency graph show that Philippine President Rodrigo Duterte is the top topic during the period selected. 

### 5. Feature Extraction
Features were extracted from the article corpus using a term frequency-inverse document frequency (TF-IDF) vectorizer was implemented, via scikit-learn’s `Tfidfvectorizer`. As opposed to an equal weighting vectorizer, the TF-IDF statistic measures how important a word is to the document and the corpus. 

[Table 2](#table2) shows the additional parameters that were taken into consideration: 

<a id="table2"></a>
#### Table 2. Hyperparameters used in the TF-IDF vectorizer
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Description</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>min_df</code></td>
<td>ignore terms that have a document frequency strictly lower than the given threshold</td>
<td>0.001</td>
</tr>
<tr>
<td><code>max_df</code></td>
<td>ignore terms that have a document frequency strictly higher than the given threshold</td>
<td>0.7</td>
</tr>
<tr>
<td><code>ngram_range</code></td>
<td>The lower and upper boundary of the range of n-values for different n-grams to be extracted. All values of n such that min_n <= n <= max_n will be used</td>
<td>(1,3)</td>
</tr>
</tbody>
</table>


The `TFidfVectorizer` performs further cleaning of the data by removing both frequent words and rare words. *Stopwords*, or words that appear too frequently in the English and Filipino language (e.g., the, a, an, and, or), were dropped from the corpus. Rappler-specific stopwords, or words that appear in more than 70% of the titles, were also ignored by setting the `max_df` parameter of `TFidfVectorizer` to `max_df = 0.7`.

Rare words, or words that appeared in less than 0.1% of the Rappler articles, were also excluded from the corpus. This was implemented by setting the `min_df` parameter of the `TFidfVectorizer` to `min_df = 0.001`.

Unigrams, bigrams, and trigrams were extracted as part of the vocabulary by setting the `ngram_range` parameter of the `TFidfVectorizer` to `ngram_range = (1,3)`. This range of n-grams was chosen to preserve the context of certain phrases such as "Rodrigo Duterte", "Supreme Court" (n=2), and "Philippine National Police" (n=3)

After vectorization, the collection of Rappler articles has **36,254 unique items** in its vocabulary.

### 6. Dimensionality Reduction
The resulting feature set is a 10,873 by 36,254 matrix. It would be computationally expensive to perform clustering on a dataset this large. To minimize computational power,  dimensionality reduction was performed on the vectorized data via **latent semantic analysis (LSA)**. This was implemented using the `TruncatedSVD` class of `sklearn`.

As a general rule for LSA, fewer dimensions allow for broader comparisons of the themes contained in a collection of text, while a higher number of dimensions enable more specific comparisons of themes. A dimensionality between 50 and 1,000 are suitable depending on the size and nature of the document collection. Sensitivity analysis was performed to identify the optimum number of components. The sensitivity analysis started with 50 components up until 1000 components, with steps of 50.  The analysis observed using n = 300 components extracted the broader underlying themes.

### 7. Unsupervised Clustering
To extract the underlying themes of the Rappler news articles, unsupervised clustering using k-means algorithm was implemented on the reduced dataset. Sensitivity analysis was performed using different cluster counts, ranging from k=2 to k=20. Selecting the optimum number of clusters relied on examining the internal validation criteria: (1) minimizing the Intracluster to Intercluster distance ratio, (2) maximizing the Calinski-Harabasz score, (3) maximizing the Silhouette coefficient, and (4) minimizing the sum of square distance to centroids coefficient. 

The optimum value of cluster counts and the resulting article clusters will be discussed in the next section.

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
[1] <a id='ref1'></a>"Duterte says he banned Rappler due to 'twisted' reporting", [https://www.rappler.com/nation/197230-duterte-rappler-ban-twisted-reporting](https://www.rappler.com/nation/197230-duterte-rappler-ban-twisted-reporting)

[2] <a id="ref2"></a>"Duterte calls Rappler 'fake news outlet", [https://www.rappler.com/nation/193806-duterte-fake-news-outlet](https://www.rappler.com/nation/193806-duterte-fake-news-outlet)

[3] [https://towardsdatascience.com/all-the-news-17fa34b52b9d](https://towardsdatascience.com/all-the-news-17fa34b52b9d)

[4] [https://seangtkelley.me/blog/2018/01/03/news-article-clustering](https://seangtkelley.me/blog/2018/01/03/news-article-clustering)

[5] [https://scikit-learn.org/stable/auto_examples/text/plot_document_clustering.html#sphx-glr-auto-examples-text-plot-document-clustering-py](https://scikit-learn.org/stable/auto_examples/text/plot_document_clustering.html#sphx-glr-auto-examples-text-plot-document-clustering-py)

[6] [http://www.scholarpedia.org/article/Latent_semantic_analysis](http://www.scholarpedia.org/article/Latent_semantic_analysis)