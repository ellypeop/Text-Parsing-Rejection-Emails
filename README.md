# Text-Parsing-Rejection-Emails
Masters coursework analysing a [rejection email dataset](https://www.kaggle.com/datasets/sethpoly/application-rejection-emails) <br>
[Inspiration and code samples](https://towardsdatascience.com/i-built-a-reject-not-reject-email-classifier-for-my-job-applications-844a3b6cd67e) <br>
The analysis up to the first Word2Vec model was set out by the university, any work after this was independent exploration into the dataset

## Python Packages

- Python version 3.12
- jupyter 1.1.1
- pandas 2.2.2
- gensim 4.3.3 (install before numpy)
- nltk 3.9.1
- numpy 1.26.4
- matplotlib 3.9.2

## NLTK Downloader

This only needs to be run once and can be commented out afterwards. When run in Pycharm a dialogue box appears, download all packages and close the dialogue once complete.
To complete the process without GUI press d for download, when asked which package to download type book, then type q to quit once the installation is complete. 


## Boxplot Explanation

A boxplot was selected for quantitative data comparison of token lengths between the two rejection statuses, the choice being its ability to convey high-level numeric information at a glance. The whiskers extending out of the box depict a minimum and maximum token length for each status. The median value is the combination of a notch and an orange line in the box. The mean token length is depicted with a green diamond. Outliers, notably only in the not_reject email status, are shown as red dots. The lower and upper quartiles are the leftmost and rightmost sections of the box, representing the token lengths before and after the median value. Their edges are calculated by a new median value of their respective groups. 

The variation in token length is greater in the non_reject emails having the lowest and highest min/max token values. As mentioned this category also contains outliers whilst the reject email does not, meaning there are some email instances with significantly higher token lengths. The mean token length is much closer to the median in the reject emails with the overall impression that the reject emails have a more consistent pattern of token length overall and therefore a more uniform structure to their emails. 

## Mean Lexical Richness

There is an insignificant difference in the mean lexical richness for each rejection status with both at 0.72%. There is a slightly higher count of richness in the not-reject emails which remains consistent with previous observations in the token lengths; not-reject emails have greater variation with a slight increase in unique tokens therefore implying a broader vocabulary. This is compared to the reject emails which have a more uniform length and a more limited vocabulary.


