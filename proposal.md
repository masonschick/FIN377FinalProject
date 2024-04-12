# Research Proposal: How Accurately Do Inverted Yield Curves Predict Recessions?
By Minh Nguyen, Mason Schick, Rebecca Zamsky, Alicia Zhang

## Research Question

**What do we want to know or what problems are we trying to solve? As in the midterm, you should list (1) the “bigger” question/debate/problem you’re interested in, and also (2) the specific research question(s) you’ll actually try to answer.**
- **The research question will be smaller in scope than the big picture question. But the answer to your specific research question should shed light on the bigger question (although it likely won’t conclusively answer it).**

The bigger question our team is interested in addressing is how various leading indicators of recessions are related with the actual performance of the economy and how accurately they precipitate recessions. We are specifically going to focus on “red flags'' in economic data that can reliably indicate an upcoming recession. Our main focus will be on analyzing yield curve data. We have observed that historically, inversions in the yield curve have consistently preceded recessions. We are interested in analyzing the data to determine if higher short term yields is one of the most important and reliable ways to measure an upcoming recession, or if there is a more important indicator(s) that causes both the yield curve inversions and recessions. Put simply, our research question is: Does an inverted yield curve precipitate a recession?
Once we are able to explore this relationship, we will expand our analysis to include other important factors like inflation rates, CPI, and the strength of the dollar compared to other currencies

**If your project is about relationships, what are the hypotheses you’re testing?
If your project is about prediction, what are your metrics of success? (What are you maximizing?) Can you find a baseline from prior work to give you a ballpark to aim for?**

The main goal of our project is to predict recessions, but we will need to analyze the relationships between various recessionary indicators to confidently make these predictions. Our hypothesis is that inverted yield curves have a greater influence on recessions than other common leading indicators. If there continues to be a correlation between an inverted yield curve preceding recessions in the future, we deem the project successful. When we run a regression, if our R^2 metric is 0.6 or higher we will conclude that it is a good predictor of a recession. We also will compare the R^2 values between inverted yield curve and the other variables we choose to add on later on in this project such as CPI, inflation rate, and strength of U.S. dollar. If the inverted yield curve outperforms at least two of these variables in terms of R^2 value, we will consider it a robust predictor of recession



## Necessary Data

**What does the final dataset need to look like (mostly dictated by the question and the availability of data):**

The final dataset will have various variables relating to the yield curve and common recession indicators. We already imported three CSV files from FRED: 
- The 10 year yield minus the 2 year yield from 1976-2024 (12488 Observations)
- The 10 year yield minus the 3 month yield from 1982-2024 (11029 Observations)
- The 10 year yield minus the fed funds yield from 1962-2024 (16247 Observations)

Since the yield curve is interrelated with the fed funds rate decisions, we will also try to incorporate some of the data they utilize such as: Inflation data, Unemployment data, and GDP data.


**What is an observation, e.g. a firm, or a firm-year, etc.**
An observation is the spread-date because with each date, we’re going to observe the yield curve through different duration periods (ex. 10yr - 2yr; 10yr - 3m)

**What is the sample period?**
We are going to try to use as much historical data as possible, and the CSVs we have imported so far go as far back as 1962. So our sample period is currently 1962-2024, but this is subject to change as we find more data and merge the various sources into our final dataframe.

**What are the sample conditions? (Years, restrictions you anticipate (e.g. exclude or require some industries)**
Restrictions we anticipate are null data and years where some variables are present but others are not available.  

**What variables are absolutely necessary and what would you like to have if possible?**
Absolutely necessary variables are the date, yield-spreads, and GDP to map recession periods. We would like to incorporate inflation rate, unemployment rate, CPI, and other commonly utilized data for dealing with interest rates and recessions.

**What data do we have and what data do we need?**
We have three yield related datasets from FRED, but we need to import more non-yield related datasets. 

**How will we collect more data?**
We will collect more data as we did previously by importing CSV files from FRED. We may also use data from sites other than FRED if necessary, and will do due diligence by using EDA to check that these datasets are reliable. 

**What are the raw inputs and how will you store them (the folder structure(s) for each input type)?**
The raw inputs are going to be the CSV files we already imported from FRED, and all of the other data we have discussed incorporating. We are hoping to get the other data from FRED as well, as it has given us reliable data in CSV format so far. We are currently storing these CSVs in a folder called “data”, and we will likely continue organizing the raw inputs like this, before storing the final data frame in a new folder called “finalDF”

**Speculate at a high level (not specific code!) about how you’ll transform the raw data into the final form.**
Since not all yield curve data from FRED dates back equally, we expect similar challenges when incorporating other relevant economic data. To address this, we'll likely need to perform an inner merge, ensuring that our final dataframe includes all necessary variables with observations for each given date. Additionally, we'll need to calculate variables indicating if a recession is currently occuring. For GDP data, we may need to manipulate it to determine if the current GDP is higher or lower than the GDP levels of the previous two months. This adjustment will help us assess the direction of GDP movement and its potential impact on recession forecasting

