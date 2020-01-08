---
title: "Contextual vs Universal Meanings of Emoji: A Case Study on #MeToo vs 2016 US Election Tweets"
author: ''
date: '2019-11-01'
slug:
aliases:
categories:
  - Paper
tags:
subtitle: ""
summary: "Do emoji mean the same things across contexts? Are there universal meanings of emoji?"
authors:
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---

This paper, using emoji in tweets about the Me Too movement and the 2016 United States elections as a case study, focused on how contexts affect the meanings of emoji by examining to what extent the meanings of emoji are composed of their universal meanings versus their contextual meanings. I found that there was not enough evidence to conclude that contexts affect the meanings of emoji on average. However, at the level of individual emoji, I found varying degrees in how much each emoji’s meaning was composed of its universal meaning versus its contextual meaning.


## 1. Introduction
Emoji are ideograms that evolve from emoticons (Barbieri et al., 2016c). Emoji are commonly used in modern text communication in the same way nonverbal cues such as facial expression, gesture, and tone of voice (Tang and Hew, 2019) support face-to-face communications. The same emoji, however, can have different meanings due to several factors such as individual differences and variations in emoji rendering across platforms.

This paper focused on how contexts affect the meanings1 of emoji within a platform by examining to what extent the meanings of emoji are composed of their universal meanings versus their contextual meanings. Take the emoji blue heart in the context of American politics for example, the question would be to what extent the meaning of blue heart is related to affections (universal meanings of heart) versus to the Democratic Party (contextual meaning of the color blue).

To guide the investigation, this paper formulated two research questions: (1) how the meanings of emoji were affected by contexts on average and (2) how the meanings of individual emoji were affected by contexts. To answer these research questions, emoji in tweets were used as the case study. Specifically, two distinct topics, the Me Too movement and the 2016 United States elections, were chosen to represent effects of contexts. The vector space model (VSM), specifically word2vec model, was used to measure the meanings of emoji.

## 2. Related Work
### 2.1 Variations in Meanings of Emoji
Several studies have found that the same emoji could be interpreted and mean differently depending on several factors. In terms of individual differences, previous studies have reported gender differences (Herring and Dainas, 2018) and cultural differences (Barbieri et al., 2016b) in emoji interpretations. A large portion of studies on emoji interpretations primarily investigated crossplatform emoji interpretations and found differences in emoji interpretations based on variations in emoji rendering across platforms (e.g., Miller et al., 2016; Morstatter et al., 2017; Tigwell and Flatla, 2016).

In terms of contexts as a possible factor for variations in emoji interpretations, Miller et al. (2017) framed their research question around the topic of emoji-related miscommunication and found that textual contexts, in fact, did not help lessen the potential for miscommunication from interpreting emoji. It is still unclear, nevertheless, how contexts affect emoji meanings and interpretations beyond the topic of miscommunication.

On the other hand, variations in meanings of emoji are often ignored in emoji-related NLP research. Miller et al. (2016) critiqued this gap in the field as follow:

> “Less is known about the consistency of emoji interpretation. Researchers such as Liu et al. (2012) and Novak et al. (2015) have developed classifiers of emoji sentiment by labeling emoji with the sentiment of the surrounding text. While this has proven largely effective, both papers mentioned instances of emoji being associated with different, and occasionally opposite, sentiment labels.”

Indeed, although most emoji-related NLP research incorporated textual contexts into their embedding spaces for emoji meanings, those spaces allowed only a single embedding to be corresponded with each emoji. Eisner et al. (2016) went even more extreme by disregard all textual contexts and solely relied their space of emoji meanings on emoji descriptions in the Unicode emoji standard. However, if emoji meanings are significantly affected by contexts as I hypothesized, it may be beneficial for emoji-related NLP tasks to allow multiple embeddings of each emoji as BERT (Devlin et al., 2018) allows each word.

Due to these gaps in the field, I believe it is crucial to better understand how contexts affect emoji meanings. 

### 2.2 Vector Space Model
Several emoji-related NLP research (e.g., Wijeratne et al., 2017a; Barbieri et al., 2016c; Chen et al., 2018) as well as some studies on emoji meanings and usages (Barbieri et al., 2016a; Morstatter et al., 2017; Wijeratne et al., 2017b) employed the skip-gram neural embedding model introduced by (Mikolov et al., 2013) as their VSMs. Hence, in this study, I implemented the same variation of VSM through word2vec module in the gensim library.

word2vec has an expectation that not only similar words will be close to each other, but that words can have multiple degrees of similarity (Mikolov et al., 2013). Hence, word2vec yields better quality of representations, especially for similarity tasks, than general N-gram models. In addition, word2vec can capture meanings beyond syntactic regularities (Mikolov et al., 2013) such that simple algebraic operations can be performed using a word offset technique.

## 3. Method
### 3.1 Data
To answer the research questions, I combined two datasets of tweets in distinct contexts: 28,629 English tweets about the Me Too movement with the hashtag #MeToo (dat, 2019), and 393,764 tweets about the 2016 United States elections on the election day(King, 2019). Only tweets in English language with at least one emoji were kept for simplification. Hence, there were 1,479 eligible #MeToo tweets and 20,959 eligible election tweets. To match the number of eligible #MeToo tweets, 1,479 election tweets were randomly sampled from 20,959 eligible election tweets and used in subsequent analyses.

\#MeToo tweets: 75.12% of #MeToo tweets in the sample contained only one emoji, 15.75% contained two emoji, 5.47% contained three emoji, and 3.65% contained 4 or more emoji. The average number of emoji per tweet was 1.41. The most frequent emoji used in #MeToo tweets in the sample were red heart (n = 259), broken heart (n = 117), and pensive face (n = 72).

Election tweets: 60.58% of election tweets in the sample contained only one emoji, 19.13% contained two emoji, 10.68% contained three emoji, and 9.60% contained 4 or more emoji. The average number of emoji per tweet was 1.90. The most frequent emoji used in the election tweets in the sample were face with tears of joy (n = 418), person with folded hands (n = 99), and heavy black heart (n = 89).

Tweets Preprocessing: During the tokenization, all user mentions, URLs, and other irrelevant information were removed from the sample tweets by excluding all tokens started with @, http, &amp and &. English stop words from nltk.corpus were used to remove all stop words from the tweets. Leading and trailing punctuation as well as digits were also removed. Lastly, all word tokens were converted to lower cases while all emoji tokens were converted to upper cases. Each emoji token was represented by its name as defined by emoji library (e.g., SMILING FACE for ,).

### 3.2 Analytical Approaches
To investigate whether contexts affect the meanings of emoji and to what extent the meanings of emoji are composed of their universal meanings versus their contextual meanings, I examined how emoji were affected by contexts on average and individually.

To perform my examinations, I started by constructing a combined VSM (hereafter, ’cVSM’) using word2vec. Specifically, tokens are constructed from the combined sample of #MeToo and election tweets, whereby emoji were tagged by their contexts (, in #MeToo tweets was tagged as SMILING FACE (metoo) while , in election tweets was tagged as SMILING FACE (election)) but not other words (“everyone” in #MeToo tweets was treated as the same token as “everyone” in election tweets). I used cVSM instead of a separated VSM for each context because meanings in VSM are derived from the corpus and thus context sensitive.

#### 3.2.1 How emoji were affected by contexts on average
To examine how emoji were affected by contexts on average, I performed a hypothesis test under the null hypothesis that emoji were not affected by contexts. First, I generated a cVSM under the null hypothesis (hereafter, ’null cVSM’). Specifically, I randomized the tags of the emoji regardless of their original tags (as #MeToo or election) such that 1,479 tweets were assigned into each group of tweets. Through the random assignment, the first group of tweets in the null corpus consisted of 746 originally #MeToo tweets and 733 originally election tweets, and vice versa for the second group of tweets in the null corpus. Newly assigned tweets, then, were used to generate the null cVSM.

After constructing both the original cVSM and the null cVSM, for each cVSM, I calculated the similarity scores of the pairs of same emoji with one emoji tagged as one context and the other tagged as another context (hereafter, ’emoji pair’; Figure 1). Then, I performed a one-sided pairwise t-test where I reject the null hypothesis if the similarity score of the emoji pair in the original cVSM is lower than the similarity score of the same emoji pair of the null cVSM.

![](/img/diagram.png)
Figure 1: Diagram of how hypothesis test was conducted.

#### 3.2.2 How emoji were affected by contexts individually
To examine how emoji were affected by contexts individually, I used two approaches. In the first approach, I examined the distribution of similarity scores of emoji pairs to similarity scores of all possible pairs of tokens in the original cVSM. In the second approach, I qualitatively examined the nearest neighbors of selected emoji pairs in three different VSMs: original cVSM, VSM trained on #MeToo tweets only, and VSM trained on election tweets only.

## 4. Results 
### 4.1 How emoji were affected by contexts on average
I could not reject the null that emoji were affected by contexts on average; from the sample, the mean of the difference distribution was 0.0003 with 95% confidence interval of -0.0001 to 0.0007 (Figure 2). This suggested there was not enough evidence to conclude that contexts affect the meanings of emoji on average.

![](/img/null_diff.png)
Figure 2: Distribution of each emoji pair’s difference between the similarity score calculated from the original cVSM and the one calculated from the null cVSM with the outlier labeled.

### 4.2 How emoji were affected by contexts individually
Figure 3 examined the distribution of similarity scores of emoji pairs to similarity scores of all possible pairs of tokens in the original cVSM. On average, a pair of tokens in the original cVSM had a very high similarity score (mean = 0.9965). Hence, it is not surprising that all emoji pairs had the similarity scores higher than 0.99. Around half of the emoji pairs had lower similarity scores than the mean. Specifically, rose, persevering, and hugging face pairs had similarity scores one standard deviation below the mean. The other half of the emoji pairs had higher similarity scores than the mean. In fact, around a quarter of the emoji pairs had higher similarity scores than the mode. From the huge spread of the emoji pairs’ similarity scores, even though on average we could not reject the null in 4.1, there were some emoji that were affected by the contexts more while some were affected less than the others.

![](/img/actual_dist.png)
Figure 3: Distribution, with mean and standard deviation labeled, of the similarity scores of all possible pairs of tokens overlapped with the similarity scores of emoji pairs in the original cVSM.

To understand the variations of contextual effects on emoji meanings in different emoji better, I examined the nearest neighbors of blue heart, eyes, and persevering face which respectively had high, moderate, and low similarity scores in 3. Figure 4 showed the nearest neighbors of each emoji from three different VSMs: original cVSM, separated VSM trained on #MeToo tweets only, and separated VSM trained on election tweets only. The nearest neighbors from cVSM were drawn in two sets: one as the neighbors of #MeToo-tagged emoji and another as the neighbors of election-tagged emoji. The top 20 nearest neighbors were drawn from each separated VSM and from each tagged emoji in cVSM. In total, there were 4 sets of 20 nearest neighbors for each emoji.

![](/img/venn.png)
Figure 4: The top 20 nearest neighbors for 1) #MeToo-tagged emoji in cVSM, 2) election-tagged emoji in cVSM, 3) emoji in VSM trained on #MeToo tweets only, and 4) emoji in VSM trained on election tweets only. The three emoji were blue heart (top), eyes (middle), and persevering face (bottom) sorted by emoji pairs’ similarity scores from high to low.

For blue heart, there were several nearest neighbors shared among the sets. Specifically, the term “I’m” was in all 4 sets. As expected, #MeToo (combined) set shared many nearest neighbors with #MeToo (separated) set, and the same went with the election (combined) and the election (separated) sets. Nearest neighbors that cVSM did not capture but the separated ones did were semantically specific such as “assault” and “sexual” in #MeToo, and “trump” in election. Most of the shared nearest neighbors between the tagged blue hearts in cVSM themselves seemed to be more semantically general. Interestingly, there were some nearest neighbors shared between #MeToo (separated) and election (combined) sets and between #MeToo (combined) and election (separated) sets: “want” and “world” respectively. These overlaps between unexpected pairs of sets further supported that blue heart was less affected by the contexts.

For eyes, there were less overlaps among the sets. Specifically, there was no nearest neighbor shared by all 4 sets. Nearest neighbors shared between the tagged eyes in cVSM were more semantically specific to election. Interestingly, #MeToo (combined) set contained many election-oriented terms that captured by neither the election (combined) nor the election (separated) set. Nevertheless, #MeToo (combined) set decently captured semantic meanings of #MeToo as there were significant shares between #MeToo (combined) and #MeToo (separated) sets. The overlaps between #MeToo (separated) and the election (combined) were also interesting; they were more semantically general. These observations suggested that eyes was more affected by the contexts than blue hearts, but there were still some universal meanings of eyes in effect across different contexts.

For persevering face, there was virtually no shared 20 nearest neighbors between the tagged persevering faces in cVSM. On the other hand, the shares between #MeToo (combined) and #MeToo (separated) sets and between the election (combined) and the election (separated) sets were very high. It is clear that in comparison to blue heart and eyes, the meanings of persevering faces were strongly affected by the contexts.

## 5. Discussion
This paper investigated how contexts affect the meanings of emoji by examining to what extent the meanings of emoji are composed of their universal meanings versus their contextual meanings.

At aggregated level, there did not seem to be any contextual influences on emoji meanings as I failed to reject the null in 4.1. However, through closer examinations on individual emoji, there were variations in how much each emoji’s meanings were composed of their universal meanings versus their contextual meanings. Some emoji were affected less by contexts and thus their meanings remained similar in #MeToo and election tweets. On the other hand, some emoji were affected more by contexts and their meanings changed significantly when they were in #MeToo versus in election tweets.

Through posthoc and qualitative observations, meanings of emoji that remained similar across contexts tended to be more general, such as “I’m”, “many”, and “it”. In contrast, meanings of emoji affected more by contexts were more semantically specific, such as “#metoo” and “trump”. From these results, it is possible that universal meanings of emoji were more syntactic and semantically general, while contextual meanings of emoji were more semantically specific.

There were, however, several limitations to this study. Firstly, the size of the sample was very small. This significantly decreased the statistical power to reject the null that contexts do not affect emoji meanings. In addition, some possible emoji pairs were not examined because of the lack of matching pairs in the other context (e.g., red heart was not examined because it was only presented in the #MeToo tweets sample but not in the election tweets sample). Hence, the results were not the complete picture of all emoji.

Secondly, the sub-samples representing each context were not symmetric in their qualities related to emoji. The average number of emoji per tweet was lower for #MeToo tweets sub-sample than for election tweets one. Besides, the same emoji often had unequal frequencies in #MeToo tweets and in election tweets sub-samples. These asymmetries could confound the results. Controlling the sub-samples to only differ in contexts but not in other qualities related to emoji could be a solution to this limitation, but the controlled sub-samples will not be representative of the real-world emoji usages. Alternatively, we can control cVSM at the algorithm level such that it is more robust to these asymmetries.

Lastly, significant portions of the analytic approaches were qualitative and hence could be subjected to biases. Moreover, if the sample size had been significantly larger, qualitative approaches would not be efficient.

## 6. Conclusion and Future Works
This paper, using emoji in tweets about the Me Too movement and the 2016 United States elections as a case study, found that there was not enough evidence to conclude that contexts affect the meanings of emoji on average. However, at the level of individual emoji, there were variations in how much each emoji’s meaning was composed of their universal meanings versus their contextual meanings

It is still unclear, however, whether this inability to reject the null was due to the small sample size or not. In addition, this result is not a complete picture and a completely objective conclusion since not all possible emoji were included in the analyses and not all analyses were quantitative.

For future works, below are some possible ideas to extend this study:
* increase the sample size as well as the variety in contexts
* control for asymmetries in the sub-samples’ qualities related to emoji
* develop quantitative methods to replace qualitative approaches used in this study
* further investigate why some emoji are more affected by contexts versus universal meanings that the others
* further investigate what types of emoji meanings are more likely to be contextual versus universal

## References
2019. Tweets with emojis - #metoo (2017-10-16) - dataset by hamdan.

Francesco Barbieri, Luis Espinosa-Anke, and Horacio Saggion. 2016a. Revealing patterns of twitter emoji usage in barcelona and madrid. Frontiers in Artificial Intelligence and Applications. 2016;(Artificial Intelligence Research and Development) 288: 239-44.

Francesco Barbieri, German Kruszewski, Francesco Ronzano, and Horacio Saggion. 2016b. How cosmopolitan are emojis?: Exploring emojis usage and meaning over different languages with distributional semantics. In Proceedings of the 24th ACM international conference on Multimedia, pages 531–535. ACM.

Francesco Barbieri, Francesco Ronzano, and Horacio Saggion. 2016c. What does this emoji mean? a vector space skip-gram model for twitter emojis. In Calzolari N, Choukri K, Declerck T, et al, editors. Proceedings of the Tenth International Conference on Language Resources and Evaluation (LREC

2016); 2016 May 23-28; Portoroz,ˇ Slovenia. Paris: European Language Resources Association (ELRA); 2016. p. 3967-72. ELRA (European Language Resources Association).

Jing Chen, Dechuan Yang, Xilian Li, Wei Chen, and Tengjiao Wang. 2018. Peperomia at semeval-2018 task 2: vector similarity based approach for emoji prediction. In Proceedings of The 12th International Workshop on Semantic Evaluation, pages 428–432.

Jacob Devlin, Ming-Wei Chang, Kenton Lee, and Kristina Toutanova. 2018. Bert: Pre-training of deep bidirectional transformers for language understanding.

Ben Eisner, Tim Rocktaschel,¨ Isabelle Augenstein, Matko Bosnjak,ˇ and Sebastian Riedel. 2016. emoji2vec: Learning emoji representations from their description. arXiv preprint arXiv:1609.08359.

Susan C Herring and Ashley R Dainas. 2018. Receiver interpretations of emoji functions: A gender perspective. In Proceedings of the 1st International Workshop on Emoji Understanding and Applications in Social Media (Emoji2018). Stanford, CA.

Ed King. 2019. Election day tweets.

Kun-Lin Liu, Wu-Jun Li, and Minyi Guo. 2012. Emoticon smoothed language models for twitter sentiment analysis. In Twenty-sixth aAAI conference on artificial intelligence.

Tomas Mikolov, Kai Chen, Greg Corrado, and Jeffrey Dean. 2013. Efficient estimation of word representations in vector space. arXiv preprint arXiv:1301.3781.

Hannah Miller, Daniel Kluver, Jacob Thebault-Spieker, Loren Terveen, and Brent Hecht. 2017. Understanding emoji ambiguity in context: The role of text in emoji-related miscommunication. In Eleventh International AAAI Conference on Web and Social Media.

Hannah Miller, Jacob Thebault-Spieker, Shuo Chang, Isaac Johnson, Loren Terveen, and Brent Hecht. 2016. “blissfully happy” or “ready tofight”: Varying interpretations of emoji.

Fred Morstatter, Kai Shu, Suhang Wang, and Huan Liu. 2017. Cross-platform emoji interpretation: analysis, a solution, and applications. arXiv preprint arXiv:1709.04969.

Petra Kralj Novak, Jasmina Smailovic,´ Borut Sluban, and Igor Mozeticˇ. 2015. Sentiment of emojis. PloS one, 10(12):e0144296.

Ying Tang and Khe Foon Hew. 2019. Emoticon, emoji, and sticker use in computer-mediated communication: A review of theories and research findings. International Journal of Communication, 13:27.

Garreth W Tigwell and David R Flatla. 2016. Oh that’s what you meant!: reducing emoji misunderstanding. In Proceedings of the 18th international conference on human-computer interaction with mobile devices and services adjunct, pages 859–866. ACM.

Sanjaya Wijeratne, Lakshika Balasuriya, Amit Sheth, and Derek Doran. 2017a.  Emojinet: An open service and api for emoji sense discovery. In Eleventh International AAAI Conference on Web and Social Media.

Sanjaya Wijeratne, Lakshika Balasuriya, Amit Sheth, and Derek Doran. 2017b. A semantics-based measure of emoji similarity.  In Proceedings of the International Conference on Web Intelligence, pages 646–653. ACM.
