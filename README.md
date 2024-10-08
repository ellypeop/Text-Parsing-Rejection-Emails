# Text-Parsing-Rejection-Emails
Masters coursework analysing a [rejection email dataset](https://www.kaggle.com/datasets/sethpoly/application-rejection-emails) <br>
[Inspiration and code samples](https://towardsdatascience.com/i-built-a-reject-not-reject-email-classifier-for-my-job-applications-844a3b6cd67e) <br>

# Introduction 

This Jupyter workbook explores patterns within a dataset of 129 job rejection emails, categorized as either “reject” or “non_reject.” The dataset has a nearly balanced distribution: 65 emails were labelled as "reject" and 64 as "non_reject."

# Python Version & Packages

- python 3.12
- jupyter 1.1.1
- pandas 2.2.2
- gensim 4.3.3 (install before numpy)
- nltk 3.9.1
- numpy 1.26.4
- matplotlib 3.9.2
- transformers 4.44.2
- seaborn 0.13.2
- pytorch [installation instructions for your system found here](https://pytorch.org/get-started/locally/)

run "pip install -r requirements.txt" in the terminal to install the packages required for this project

# NLTK Downloader

This only needs to be run once and can be commented out afterwards. When run in Pycharm a dialogue box appears, download all packages and close the dialogue once complete.
To complete the process without GUI press d for download, when asked which package to download type book, then type q to quit once the installation is complete. 

# Section A - University Guided Analysis

## Boxplot Explanation

A boxplot was selected for quantitative data comparison of token lengths between the two rejection statuses, the choice being its ability to convey high-level numeric information at a glance. The whiskers extending out of the box depict a minimum and maximum token length for each status. The median value is the combination of a notch and an orange line in the box. The mean token length is depicted with a green diamond. Outliers, notably only in the not_reject email status, are shown as red dots. The lower and upper quartiles are the leftmost and rightmost sections of the box, representing the token lengths before and after the median value. Their edges are calculated by a new median value of their respective groups. 

The variation in token length is greater in the non_reject emails having the lowest and highest min/max token values. As mentioned this category also contains outliers whilst the reject email does not, meaning there are some email instances with significantly higher token lengths. The mean token length is much closer to the median in the reject emails with the overall impression that the reject emails have a more consistent pattern of token length overall and therefore a more uniform structure to their emails. 

## Mean Lexical Richness

There is an insignificant difference in the mean lexical richness for each rejection status with both at 0.72%. There is a slightly higher count of richness in the not-reject emails which remains consistent with previous observations in the token lengths; not-reject emails have greater variation with a slight increase in unique tokens therefore implying a broader vocabulary. This is compared to the reject emails which have a more uniform length and a more limited vocabulary.

# Section B - Independent Exploration and Analysis

## Name Addressing

The first analysis counted emails where the recipient, Seth, was addressed by his first name to assess the level of personalisation. The results showed 11 instances in rejection emails and 14 in non-rejection emails. Additionally, 2 rejection emails misspelled Seth’s name as "eth." A bar chart was chosen for its efficiency in conveying quantitative information. The lower frequency of name usage and the incorrect spelling in rejection emails highlight a lack of personalisation in the rejection emails.

## Boxplot Values

The second investigation focused on obtaining the exact figures from the earlier boxplot, which provided an overview of token lengths in rejection and non-rejection emails.

Accessing these exact values opened up several opportunities for deeper dataset exploration. Analysing the outliers was considered however, due to these only existing within the non-rejection emails, it would not present any findings which could be compared between the two email types. Instead, by observing the minimum token counts from each email type, two instances were selected with a similar token count, 20 and 22, to build parser trees and explore their grammatical construction.

## Token Parsing

Preprocessing was applied to remove punctuation and empty strings.  Neither Stemming nor Lemmatization was required for these emails as they consisted of unique tokens, therefore already existing in their root form. POS tagging was applied and observations were made with and without stop word removal due to concerns that it may prove counterintuitive when analysing the sentence grammar.

Some noteworthy observations made were “PatientsLikeMe” being incorrectly classed as an adjective, perhaps due to the capitalisation removal. “Seth” was also incorrectly classified as a verb. Issues did arise with the removal of stop words specifically with the rejection email instance; “not” is removed which had serious implications for the context behind the email. “Engineer” was changed from a noun to a verb once stop words were removed. This could be due to the removal of “with your" indicating it is an action rather than a string of possessive nouns.
 
The RegexpParser was used to define grammatical patterns in the instances using regular expressions indicating whether the POS can be optional (?) repeated (*) or contain multiples of a similar type (V. = VB, VBN, VBZ etc) [Source for regular expressions symbols](https://pythonprogramming.net/regular-expressions-regex-tutorial-python-3/). 

The baseline structure for the RegexParser was obtained from [a Stack Overflow query](https://stackoverflow.com/a/71492485/23331537) and built upon by analysing the POS tags  to consider the numerical values in the non-rejection email, optional consideration of adverbs in the rejection email, and repeated nouns due to the noun string “Full Stack Software Engineer Application” [Source for POS tags](https://pythonprogramming.net/natural-language-toolkit-nltk-part-speech-tagging/)

The clarity of the non-rejection email is retained with and without the stop word removal. This is due to the matter of fact nature the email possesses where the purpose is to convey to the recipient that a financial statement, within a specific time frame, has been generated.

The same cannot be said for the rejection email. Observing the structure where stop words have been removed, the exclusion of “not to” gives the email an entirely different meaning. Excluding the token “unfortunately” it could be confused for an acceptance email. A newly constructed “engineer application” verb phrase has been created due to the inaccurate classification of “engineer”. The prepositional phrase “at this time” is entirely lost resulting in “time” without any context. When the stop words are removed in the rejection email it becomes nonsensical.
 
The contrast between these two examples indicates that a non-rejection email has the luxury to be matter-of-fact whereas a rejection email is constricted to using “gentle” language. The use of phrases like “move forward” being proactive and “at this time” encouraging hope for a successful application in the future, gives an overall positive tone which betrays the true intent of the message.  The rejection email depends on stop words to convey its meaning or to retain its original context.
 
The results from these two case samples imply that issues could arise where stop word removal is applied to the whole dataset before analysis. The intention of the email can be inadvertently changed. This brings us to our final experiment where we observe the positive, negative and neutral sentiment of the entire dataset.

## Sentiment Analysis

The VADER NLTK module and RoBERTa transformer module were used to compare sentiment analysis across the dataset. VADER assigns a sentiment score to each token which is then aggregated to assess the overall sentiment of the email. RoBERTa, an improved variant of the BERT model,  is a pre-trained neural network used for sentiment analysis. It is considered to have better accuracy due to its ability to capture the context and relationship between words.[Source 1](https://medium.com/@rslavanyageetha/vader-a-comprehensive-guide-to-sentiment-analysis-in-python-c4f1868b0d2e)[Source 2](https://lup.lub.lu.se/luur/download?func=downloadFile&recordOId=9145112&fileOId=914511)
 
The scores for each model were calculated and added to the data frame. Using Seaborn the results were then visualised as a heatmap to observe the variance of sentiment counts between the different models and respective email types. A heatmap was chosen to illustrate the qualitative nature of each model's sentiment outputs.

The results show that the majority of the emails have a positive sentiment which is to be expected due to emails generally being written in a polite manner. This begs the question as to whether sentiment analysis is an appropriate tool in the remit of email analysis, however, it does allow us to explore the difficulties natural language processing techniques face when presented with a rejection email. We would assume that being rejected for a job should be indicative of negative sentiment.  

Out of the 65 rejection emails, RoBERTa detected 8 as negative, while VADER identified only 3. Analysis revealed that the token "unfortunately" was a key indicator of negative sentiment. RoBERTa successfully recognised this sentiment regardless of the keyword's position in the email, whereas VADER only detected negative sentiment when "unfortunately" appeared at the beginning. This discrepancy may be due to VADER's sensitivity to other tokens, which it might interpret as noise, while RoBERTa better accounts for contextual cues within the email. 

Both models struggled in determining rejection emails as neutral instead of negative due to the presence of positive language, with Vader classing 8 as neutral and RoBERTa classing 5 as neutral. This is surprising as RoBERTa is considered a stronger model. Its potential difficulty may stem from its contextual approach, which considers the overall context of the email rather than evaluating each word’s sentiment in isolation. Consequently, the presence of positive language may have negatively impacted RoBERTa’s ability to accurately classify the email's true intent.

In the non-rejection emails, there were notable differences in how each model assessed negative sentiment. Both models identified two non-rejection emails as negative: Vader selected emails #108 and #114, while RoBERTa chose emails #108 and #118. Email #108, an error warning, was appropriately classified as negative by both models. Email #114, which RoBERTa categorized as neutral, uses time pressure to prompt the recipient to sell an item. Vader, however, identified it as negative, potentially due to the implied urgency and pressure, which it interpreted as a negative consequence. Email #118, which Vader classified as positive, is an informative email but includes negative tokens such as "violation" and "restricted." Although a human observer might consider #118 to be neutral overall, the inclusion of negative terms justifies its classification as negative by RoBERTa. 

This comparison raises an interesting question: Was RoBERTa better at discerning the nuanced context of these emails, particularly recognising that the positive aspect of a potential sale in email #114 might overshadow the negative language? Conversely, did Vader more accurately capture the negative implications of time pressure in #114?

# Conclusion

In this analysis, we have observed that the rejection emails contained more counts of impersonalisation by addressing the recipient incorrectly. The removal of stop words can skew our results with misclassification of parts of speech resulting in a change of intention to the email. “Unfortunately” was a keyword appearing in the observed rejection emails; further exploration on this token in the data set could prove beneficial.  The sentiment of both email types was generally positive which created difficulty for both models in identifying job rejections, suggesting a different metric may be more suitable. Careful consideration of preprocessing techniques, sentiment model selection and NLP techniques is necessary to garner both accurate and valuable results from the dataset.




