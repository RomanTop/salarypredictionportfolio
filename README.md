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

Both relationships are something to be expected to see, make sense and pretty much self-explanatory.

Distribution in salaries of different types of jobs didn’t reveal anything unexpected. The highest average salaries have ‘C-suite’ types of top managers.

![](https://github.com/RomanTop/salarypredictionportfolio/blob/master/pictures/Job_type.png)

Distributions of salaries among degrees go in ascending trend – the higher degree the higher mean salary.

![](https://github.com/RomanTop/salarypredictionportfolio/blob/master/pictures/Degree.png)

Building a plot for distributions of salaries among different majors showed not much variation with the exception for people with no degree. The mean salary for them significantly lower.

![](https://github.com/RomanTop/salarypredictionportfolio/blob/master/pictures/Major.png)

The least self evident was a plot that uncovered nowadays trends in distributions of salaries depending on industry. Information technologies represented in this data set by Web industry took only the third place among other industries while the highest mean salary is still in Oil Industry.

![](https://github.com/RomanTop/salarypredictionportfolio/blob/master/pictures/Industry.png)

The further investigation in grouping any two categorical features by mean salary made even more evident combination of what factors lead to higher mean salary. These are people with a Doctoral or Master’s degree, with major in Engineering or Business who work in Finance or Oil Industries.

![](https://github.com/RomanTop/salarypredictionportfolio/blob/master/pictures/Heat_mapspng_Page1.png)
## Modeling

Before modeling I established a baseline for comparison and measuring efficacy of future models. This baseline is just a very simple predicting model and I chose Industry mean salary for this role. I calculated mean salary for each of seven Industries represented in the Data Set and saved them into a dictionary. After that I assigned to each job posting corresponding industry average salary and built a plot showing actual salaries vs. predicted

![](https://github.com/RomanTop/salarypredictionportfolio/blob/master/pictures/Baseline_model-plot.png)

Each peak represents one out of seven industries in the data set. Also is known that two industries Oil and Finance have the same mean salary, so they are stacked one over another creating one high peak. Also, as an additional information it is visually seen that proportion of job postings of each industry in the data set is roughly the same.

I chose MSE (Mean Squared Error) in order to calculate efficacy of a model. Calculating MSE for the baseline I got 1367.12 
Based on the following considerations, I chose next three algorithms for modeling:

1.	Since there is a somewhat linear relationship between numeric variables like years of experience and miles from metropolis and the target, Multiple Linear Regression can be a reasonable choice for a first predictive model.
2.	Having more than 100k observations (job postings) in the training data set and quantitative target allows to choose Stochastic Gradient Descent Regressor (SGD) as possibly more efficient model comparing to the Linear Regression.
3.	Random Forest as one of the most used algorithms provides high accuracy, handles a large proportion of data and can be used for regression tasks will be the third option for this project.

After performing necessary tasks like get dummies for categorical variables, split the data set, where I chose 0.25/0.75 test-train split, and hyperparameter grid search I calculated MSE for each model. Since SGD regressor is sensitive to feature scaling, scaling the data was recommended. In order to prevent data leakage after scaling for future 5-fold cross validation I used pipeline approach.
The results of calculating MSE during 5-fold cross validation of each algorithm are shown below:

Baseline - 1367.12

Multiple Linear Regression – 384.42

SGD Regressor - 384.59

Random Forest – 366.15

As seen Random Forest provided the best results among chosen algorithms so it was used as a production model. The plot below shows Actual vs Predicted salaries.

![](https://github.com/RomanTop/salarypredictionportfolio/blob/master/pictures/Actual_vs_Predicted.png)
