## PROBLEM STATEMENT ##

As a “hypothetical” employee of Zillow, I was tasked with creating a regression model to predict the sale price of homes in Ames, Iowa. Evaluation of the model would be done by running my model against a quarter of my subset (that I removed during my model-building phase) and comparing my predicted sale price for that “holdout” set against the actual home sale price. The benefits of this project would be the ability to determine the approximate sale price of a home given certain data about it. This model could be used by potential home sellers who want to identify what their home might sell for.

## EDA / Pre-processing##

In this section, I did the following
- addressed missing values
- removed features that I determined to be unlikely to help my model
- converted categorical values to numeric ones
- feature engineering

Based on the correlations we've seen here, I expect that we'll be able to create a model to predict home sale price.

## Pre-Processing - (continued) / Modeling (notebook 2) ##

- Concluded my pre-processing by dropping additional columns and creating a number of interactions
- Generated a number of models including
    - Linear Regression
    - Ridge
    - LASSO
    - Elastic net
- Ended up submitting using my LASSO model

## Analysis / Explanation ##

The baseline model has an around 80,000 so we definitely want our model to be better than that. However, our model is predicting home sale prices so errors in the tens of thousands should also be somewhat expected.

My approach on this project was a bit scattershot in that I started with my EDA but half-way through decided I wanted to get some modeling results and ended up guessing on or using many of the columns that I was planning on doing my EDA on. This surprisingly generated a fairly good RMSE score. I then proceeded to finish my EDA and to my suprise, ended up with a worse RMSE score. I then looked back at my first models and identified a number a columns using LASSO that had high correlations that I subsequently eliminated and proceeded to add those back in which lowered my RMSE scores. Finally, I used a LASSO regression to identify higher and zero coefficient features. I removed the zero coefficient features and ended up creating interactions for stronger coefficient features that appeared like they may be co-linear.

The result of removing the zero coefficient features caused my linear regression and Ridge model scores to be essentially the same. This makes sense since those extra coefficients were screwing up my linear regression and without them, I didn't need any regularization on my model. My elastic net regression didn't converge but showed an l1 ratio of 1 indicating pure LASSO. This means that LASSO is purely the best model for my data and not a combination of the two.

The creation of interactions makes the analysis of individual coefficients difficult to do, especially relative to other features. Instead, we can draw conclusions from the process of generating our final model. My initial thought process was to use EDA to identify correlated features and then generate a model with only those features. Through interaction using LASSO though, I realized that many of the features I didn't think had value actually ended up helping my model. I believe the reasoning for this is that features that don't appear predictive of sale price when combined with other features actually become predictive. If I was to re-do this or do this project again, I would try to remove less features prior to running LASSO and then use the results of that first run to remove features and generate interactions to iterate to a better model.