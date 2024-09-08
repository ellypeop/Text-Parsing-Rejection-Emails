# Text-Parsing-Rejection-Emails
Masters coursework analysing a [rejection email dataset](https://www.kaggle.com/datasets/sethpoly/application-rejection-emails) <br>
[Inspiration and code samples](https://towardsdatascience.com/i-built-a-reject-not-reject-email-classifier-for-my-job-applications-844a3b6cd67e)

## Python Packages

- jupyter 1.1.1
- pandas 2.2.2
- gensim 4.3.3 (install before numpy)
- nltk 3.9.1
- numpy 1.26.4
- matplotlib 3.9.2

## Boxplot Explanation

A boxplot was selected for quantitative data comparison of token lengths between the two rejection statuses, the choice being its ability to convey high-level numeric information at a glance. The whiskers extending out of the box depict a minimum and maximum token length for each status. The median value is the combination of a notch and an orange line in the box. The mean token length is depicted with a green diamond. Outliers, notably only in the not_reject email status, are shown as red dots. The lower and upper quartiles are the leftmost and rightmost sections of the box, representing the token lengths before and after the median value. Their edges are calculated by a new median value of their respective groups. 

The variation in token length is greater in the non_reject emails having the lowest and highest min/max token values. As mentioned this category also contains outliers whilst the reject email does not, meaning there are some email instances with significantly higher token lengths. The mean token length is much closer to the median in the reject emails with the overall impression that the reject emails have a more consistent pattern of token length overall and therefore a more uniform structure to their emails. 


