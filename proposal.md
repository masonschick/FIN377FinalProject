# Research Proposal: How Accurately Do Interest Rates and Other Loan Variables Predict Loan Defaults?
By Minh Nguyen, Mason Schick, Rebecca Zamsky, Alicia Zhang

## Research Question

**What do we want to know or what problems are we trying to solve? As in the midterm, you should list (1) the “bigger” question/debate/problem you’re interested in, and also (2) the specific research question(s) you’ll actually try to answer.**
- **The research question will be smaller in scope than the big picture question. But the answer to your specific research question should shed light on the bigger question (although it likely won’t conclusively answer it).**

The bigger question our team is interested in addressing is how various attributes related to loans affect the likelihood of loan defaults. So overall, we want to learn how to predict loan defaults given specifications for many important variables. More specifically, we are going to focus on a 2013 subsample of loan data from the machine learning folder. Despite the limited range of time in our data, we should be able to obtain meaningful insights about loan defaults that are likely to occur beyond the limited scope of our data. Specifically, we will be looking for the variables in our 2013 data that were the most impactful in affecting loan defaults. Put simply, our research question is: What variables surrounding loans are the most important to consider when anticipating the likelihood of defaults?
As we start to determine the most important variables that provide the most accurate indications of a default, we will continue to look at other variables in our extensive data frame to get the most accurate picture we can within our 2013 data.

**If your project is about relationships, what are the hypotheses you’re testing?
If your project is about prediction, what are your metrics of success? (What are you maximizing?) Can you find a baseline from prior work to give you a ballpark to aim for?**

The main goal of our project is to predict loan defaults, but we will need to analyze the relationships between various loan indicators to confidently make these predictions. Our hypothesis is that interest rate has the most significant impact on loan defaults compared to other common leading indicators. If there proves to be a substantial correlation between the interest rate percentage and loan defaults in the future, we will deem our hypothesis correct, but we will also analyze other variables to determine their correlations with loan defaults.

The overall model is a classification problem, so we will use sensitivity and precision analysis when evaluating the model. We will classify our outcomes in four possible categories: True Positive, True Negative, False Positive, False Negative. In this specific problem, we are most concerned with maximizing the True Positive (the person will default) and minimizing the False Negative (the person will default but we predict they do not). 

When comparing the strengths of each independent variable in relation to the credit default rate, we will use the F1 value given the imbalanced data. We will classify any variable with an F1 larger than 0.6 as a strong predictor and any variable below that a weak predictor. We will aim to find at least 3 variables that have an F1 larger than 0.6 incorporated into our model. If the F1 of the interest rate is included in those variables, and is higher than 2 of the 3 additional variables, then we conclude that our hypothesis holds true. 

## Necessary Data

**What does the final dataset need to look like (mostly dictated by the question and the availability of data):**

Taking the 2013 subsample csv provided in the machine learning folder, we have 134,804 observations of loan data with 33 data points. According to the loan status variable, of those observations, 113,780 loans are fully paid, while the remaining 21,024 are charged off (loan default). Most of these fields will have values for each observation, and have the potential to be extremely useful in the final dataset, but we will still refine the original dataframe. For example, member_id is a completely null column, so we will remove this field entirely. Additionally, ‘desc’, which lists a brief description of the loan, is null in 86076 observations, and the existing data looks less useful than other variables we will prioritize. ‘emp_length’ and ‘emp_title’ (which represent employment length and title) also have thousands of missing values, so these variables will also require further investigation.

The final dataset should utilize most of the remaining data, as it will allow more customization in the dashboard. Some variables that will certainly be in the final dataset include ‘id’ (unit of observation), ‘addr_state’, ‘annual_inc’, ‘dti’ (total monthly debt payments divided by monthly income), ‘earliest_cr_line’ (the date of the borrowers first credit), ‘emp_length’ (employment duration), ‘installment’, ‘int_rate’, ‘loan_amnt’, and ‘zip_code’. Nonetheless, we will not be limiting ourselves to these ten variables in our analysis.

**What is an observation, e.g. a firm, or a firm-year, etc.**
An observation is the ID given that each value represents a unique person and their corresponding conditions.

**What is the sample period?**
We will try to use the full length of data available, so our sample period will tentatively be from January to December 2013. This range is based off of our variable issue_d, which represents the date the loan was funded. Additionally, we will utilize ‘earliest_cr_line’, which lists the first time that debtor borrowed. These dates range from April 1955 - September 2010. It is worth noting these dates, as they extend beyond our sample period range, but they do not impact the actual dates of the loans, which is our focus.

**What are the sample conditions? (Years, restrictions you anticipate (e.g. exclude or require some industries)**
Restrictions we anticipate are null data and observations where some variables are present but others are not available. We have found that certain variables are affected by null data, including among them: member_id, emp_length, emp_title, and revol_util (the amount of the credit line used relative to total credit available). If we plan to use these variables in our prediction, we would have to account for the missing values. 

**What variables are absolutely necessary and what would you like to have if possible?**
Absolutely necessary variables are the annual income (annual_inc), subgrade, loan issue date (issue_d), loan status, and interest rate (int_rate). We would like to incorporate loan amount (loan_amnt), FICO credit score (combining FICO_range_low and FICO_range_high), purpose, earliest credit line, among other useful variables as previously stated in our description of the final dataset.

**What data do we have and what data do we need?**
We have the 2013 loan default dataset which features demographic variables related to the borrower, as well as loan characteristics. We don’t appear to need any further data given our current dataset is quite expansive in its variables available. If we find that the rest of the analysis goes smoothly, we might consider searching for more years worth of the same data, but this will depend on our progress with the initial analysis, and the availability of additional consistent data.

**How will we collect more data?**
With over 100,000 observations, we already have sufficient data to satisfy the objectives for this project. Nonetheless, if we are able to complete our analysis and dashboard in time to consider additional data, we will consider additional resources available at kaggle:

https://www.kaggle.com/code/janiobachmann/lending-club-risk-analysis-and-metrics
https://www.kaggle.com/code/faressayah/lending-club-loan-defaulters-prediction

The first project at the provided link includes a very similar dataset, but it has 887379 observations. There is also an issue_d variable with dates at least as far as December of 2011.

The second project at its provided link also includes a similar dataset, which has a total of 396030 observations. The issue_d variable there appears to range from 2007-2016. 

**What are the raw inputs and how will you store them (the folder structure(s) for each input type)?**
The raw input is going to be the CSV file we will import from our class’s provided machine learning inputs folder, which was used in a previous exercise. We will store this CSV in an input data folder called “data.”

**Speculate at a high level (not specific code!) about how you’ll transform the raw data into the final form.**
Transforming the raw data into the final form should not be as difficult as we originally expected for our original project proposal. Our revised focus is utilizing data from the machine learning folder, so we have relatively high quality raw data. However, we will still need to do typical due diligence to ensure the final form of our data frame includes only relevant data with no missing values. As we already discussed, there are several variables with many missing data points, and there will be other variables that we might consider removing as we do further analysis to understand the raw data better.

If we end up including the data from the resource we found in Kaggle, we will need to do a lot of work to only include the variables that are shared between both raw dataframes. This would require an inner merge, and likely a separate analysis entirely. Nonetheless, we must prioritize our analysis of 2013 data before we even consider incorporating another dataframe.
