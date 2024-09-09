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


