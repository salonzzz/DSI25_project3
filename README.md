# EXECUTIVE SUMMARY

## Problem Statement


Due to the COVID-19 pandemic, the ability to physcially visit facilities of any nature have become limited. Specifically, one's ability to walk into a rehabilitative facility on a whim is no longer a possibility without first being tested negative for COVID. This really de-motivates people from seeking help since their needs cannot be catered to instatenously anymore and the expected delays often put people off from seeking help altogether. 

People are cooped up at home more now and it is no surprise that the stress of having to live through such unprecedented times is catching up. People are drinking, smoking, abusing drugs more with little to no other avenues to cope with the novel situation and it is easy to go down the slippery slope of addiction. 

People who are able to catch on that they are becoming addicted to a substance often do want to seek help but given the lack of ease in seeking helping physically in these pandemic times, recovering addicts have turned to social media platforms such as reddit to air their concerns. While doing so allows them to offer recovery aid peer to peer, it still does not allow them to access professional resources just as easily.

Rehabilitative facilites, as a result, have reached out to our team of data scientists and tasked us to identify people seeking aid for addiction and specifically seeking aid to curb a smoking or drinking problem. Avenues to help are available but there is a lack of means to access professional services that can help addicts just as well as a physical visit to a rehabilitative centre might. We aim to create an online chatbox for these rehabilitative facilities such that any query put in by a user in the chatbox can instantenously be identified as a smoking or drinking problem based on the keywords being used in the query and within seconds users can be redirected to targetted professional aid to guide them along their path to recovery during these unprecedented times. 

## The process of addressing the problem statement

This details the process of creating the chatbox. 2000 posts will be scraped from subreddits r/stopsmoking and r/alcoholicsanonymous. These datasets will then be checked for duplicate posts, unwanted characters like emojis, and URLs. Identified duplicate rows will be dropped and unwanted charcters and URLs will be scrubbed from the title and selftext columns. All other columns will be dropped as we want to focus on using text posts for this classification task. A new column combinign the title and selftext will be created so as to encompass all text from a post. This will be used in our modelling process. The r/alcoholicsanonymous and r/stopsomking datasets will then first be encoded as 0 and 1 respectively before being merged.The data will then undergo pre-processing which involves removing stop words, tokenizing words and lemmatizing them. After some explaratory data analysis to attain preliminary insights, the data will be fitted and classification models such as Naive Bayes, KNearestNeighbour and Logistic Regression, will be trained on the data such that they are able to classify whether a post is from r/stopsmoking or r/alcoholics anonymous respectively when it comes to unseen data/posts. The best model or most accurate model (based on metrics such as the R2 score or Area under the curve score) to predict whether a post is made by a recovering smoker or alcoholic will then be used to construct a chatbox.

## Results and insights


| Model | Train Score | Test Score | AUC Score |
| --- | --- | --- | --- |
| Multinomial Bayes (TF-IDFVectorizer) | 0.98 | 0.95 | 0.99 |
| Logistic Regression (TF-IDFVectorizer) | 0.99 | 0.95 | 0.99 |
| KNeighborsClassifier (TF-IDFVectorizer) | 0.93 | 0.83 | 0.89 |
| Hypertuned KNeighborsClassifier (TF-IDFVectorizer) | 0.91 | 0.88 | 0.96 |

Based on the train,test and AUC scores, the TF_IDF Vectorized Multinomial Bayes is the best performing model. This indicates that it will be a good and accurate model at determinging whether a new post is from r/alcoholicanonymous or r/stopsmoking. The reason why Multinomial Bayes seems like a better model than Logistic Regression despite the equivalent test and AUC scores is because the train score for LogReg is 0.99 indicating that there might be overfitting. As a result, the findings cannot be well-generalised to unseen data/posts. 

Nonethless the 0.99 AUC score for both the Multinomial Bayes and Logistic Regression indicate that they are both well suited to predict which subreddit a post comes from. 

## Future Improvements

In subsequent reiterations of this project, a more diverse range of models including but not limited to SVM, Random Forest, GLM could be used to further test which model works best at classifying textual data. 

Apart from that, many other data cleaning improvements can be made. While URLs and emojis were delt with in this project, special characters such as the trademark sign or digits also need to be identified and removed. During preprocessing, custom stopwords can be identified i.e. non-useful predictive words -things like day/month/year from our data- and removed.

It may be worth considering exploring related subreddits such that we can better predict whether a post is being made by a recovering alcoholic or recovering smoker. We could train our model on more subreddits to make it more profficient at filterting text data put up by recovering alcoholics and recovering smokers and this can then be used to help guide recovering addicts appropriatly. 


## Conclusion

Based on the findings of this project, it becomes obvious that people are aware of their addictions and are reaching out for help on online platforms such as reddit. They seem to engage well on these topics online. However help recived on these platforms are peer to peer. Now that we have identified an algorithm that can identify whether a member of the community is seeking help for alcoholism or smoking based on the text/words they use, rehabilitative centres can benefit from having online chatboxes on their sites. These chatboxes will allow people to express what addiction they are seeking aid for in as little or many words, as specific or as generic words, that they prefer, to easily and quickly access targetted professional help for it even during these tough pandemic times. 
