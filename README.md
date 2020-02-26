# Salary Predictions Based on Job Descriptions
Salary Prediction Project (Python).
Exploring a set of job postings with salaries and then building a model to predict salaries for new job postings.
## Introduction
This project is dedicated to analysis of job postings in order to:
1.	explore relationship between attributes of a job posting and a salary for this position,
2.	based on the results of the exploration find out if salary for each job posting can be predicted and if it is possible build a model that predicts a target with a certain accuracy.

The data set is provided in two csv files 'train_features.csv' which contains attributes of each job posting and 'train_salaries.csv’ that has salaries for each corresponding job posting.

The head of the data set with job postings attributes has the following format:

![](https://github.com/RomanTop/salarypredictionportfolio/blob/master/pictures/Features_Table.png)

The head of the data set contains salaries of the job postings looks like this:

![](https://github.com/RomanTop/salarypredictionportfolio/blob/master/pictures/Salary_Table.png)

For the future operations with the data I combined two data sets into a one performing inner join using jobID as a Foreign key.

![](https://github.com/RomanTop/salarypredictionportfolio/blob/master/pictures/Head_of_df.png)

## Preprocessing

Before starting any analysis, I looked for duplicated and missing data. None of those were found in the dataset. Checking invalid data revealed 5 rows with salary value equals ‘0’ and they were removed from the dataset.

## Exploratory Data Analysis

In order to uncover any relationship between attributes and salary and among attributes themselves as well I did Exploratory Data Analysis. As a result, it revealed some strong relationship between most attributes and the target.
First of all one of the strongest relationships were found between each numeric attribute such as ‘Years of Experience’ and ‘Miles from Metropolis’ and a salary. The correlation matrix showed that quite clearly:

![](https://github.com/RomanTop/salarypredictionportfolio/blob/master/pictures/Correlation_matrix.png)

Building a plot of relationship between each of these attributes and the target also showed that a type of this relationship is almost perfectly linear but with the opposite trends for the corresponding attributes.

![](https://github.com/RomanTop/salarypredictionportfolio/blob/master/pictures/Miles_from_Metropolis.png)

![](https://github.com/RomanTop/salarypredictionportfolio/blob/master/pictures/Years_of%20Experience.png)
