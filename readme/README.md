# Problem Statement 

The year is 2011 and I am an analyst at House Flippers, Inc. 

House Flippers, Inc, is a Chicago-based firm that purchases houses in the Mid-West, renovates them, and sells them at a profit. House Flippers, Inc is expanding the regional scope of their business and has chosen Ames, IA as their next city to flip houses.    

My job is to create a predictive model that will estimate how much a house in Ames, IA will sell for based on various attributes, so House Flippers, Inc can have a better idea of how to focus their renovations and estimate their potential profit. 


# Background

As of the census of 2010, there were 58,965 people, 22,759 households.

Ames is home to the University of Iowa, which attracts many younger residents and is largest employer in the city by far. 

The dataset spans 2006 – 2010, therefore including home sales leading up to, and sometime after the Great Recession of 2008.

# Metadata

Data is sourced from the Ames Assessors Office and was originally compiled as part of a project for an undergraduate regression course. 
The dataset used to train the model contains 2051 individual home sales. 
This represents roughly 9% of the total households in the city of Ames during the time. 
The dataset contains 81 variables. 


# Data Dictionary

Original dataset documentation and data dicitonary found [here.](https://http://jse.amstat.org/v19n3/decock/DataDocumentation.txt) 

# EDA 

Based on the summary statistics of the sale price, we can see the large range of home prices from ~\$13000 to ~\$610,000. Furthermore, we can already infer that prices are postively skewed as the mean value is larger than the median.

Contrary to what's expected it seems the number of bedrooms above ground and sale price have a muted relationship. Sale price appears to actually go down with price. This may because larger homes are used to accomadate students (ie fraternity houses) which may have an inverse relationship with overall quality or general desirability. 

Two story buildings built after 1946 had the highest average sale prices, while one story homes built before 1946 had the lowest. 

The Floating Village Residential zone had the highest average sale price, but is a retirement community and does not make up a large portion of the housing stock. 

Northridge, Northridge Heights and Stonebrook enjoy the highest average home sales, while Old Town, Northwest Ames, and the Iowa Department of Transportation and Railroad are the lowest.  

Surprisingly enough, the drop in average annual sale price was not as signficat during and after 2008 as one might have expected, indicating that Ames housing is recession-proof, most likely due to the presence of the university, which provides a steady flow of residents despite economic down-turn.

Sale price varies widely on a monthly scale – homes sold in January sell for more than \$30000 than a home in April, on average. More than four times the amount of homes are sold in the summer than in the winter on average, annually.

Sales prices are positively skewed. Because they are not normally distibuted, this may affect its predictive power when being used for modeling. Overall quality, which sale price is most closely correlated, is negatively skewed.

The recency of a home's building or remodeling has a linear, but also diluted relationship to sale price. The greater living area column has a high correlation with sale price and exhibits a clearly linear, but varibale realtionship.

# Modeling

## Intial Benchmarks

Admittedly, the work flow of the project has been more sporadic and cyclical than linear. 
There were two previous model iterations using different selections of features, which were not documented properly, and instead were simply replaced with the most recent. 

Our true baseline score comes from the inital OLS model, which used the 45 most correlated variables in terms of absolute value to the target, sale price. Multicollinearity was note accounted for and no features were removed. This model had a training score roughly 0.87, a test score of 0.82, with an RMSE of approximately \$32,000 – discernibly overfit and not very accurate. 

The next model took a similar approach, but with an attempt to mitigate high variance. Using the same intitial list of correlation by absolute value, 30 features were picked, and further shaved down to remove obviously collinear variables such as garage area and garage car capacity, amongst others. This model had a training score of 0.77, test score of 0.73, with an RMSE of approximately \$41,000 just about as overfit as the intial model and even less accurate. 

# Interpretation

The current model started the same as the previous iterations, but collected the 65 features most correlated to the target. Clearly collinear variables were removed by hand in this iteration as well. With high trainging, test scores and small difference between the two this model seemed to provide the most accuracy while simultaneously mitigating overfitting. Additionally, with an RMSE of \$25270 it has the RMSE so far. 

Even after implementing the features through a variety of models, the original OLS model has the best trade off in terms of the highest score and second lowest difference between scores, and therefore will be used as the production model. Holding all else constant and based on the given variables in the OLS model, we can predict with approximately 90% accuracy how much a house would have sold for in Ames, IA from 2006-2010, within a roughly \$26000 range.

# Assumptions 

Based on the value of correlations to the target, we will assume there is a linear relationship to be explored. However, based on the collective influence of houses within a given proximity, assuming that samples behave independently may be a stretch in this instance. We will assume our residuals loosley follow a normal distribution based on the histogram above. However, our residuals do not exhibit homoskedasticity as the residuals are not random but follow a pattern of greater variability as the sale price increases.  

# Recommendations & Conclusions

## Building Reccomendations

The overall quality of the building was the most highyl ocrrealted with sale price, additonally, a surplus of living, garage, and basement space helped add value. Newer buildings, the presence of a poured concrete foundations and stone masonry were also price boosters. 

Steer clear of buiildings that have poor exteriors, low quality ktichens, and no fire places. Detached/unfinished garages, as well as cinder block foundation were also seen to hurt the average sale price of a home.  

## Location Reccomendations

Aim to buy houses in neighborhoods such as Northridge, Northridge Heights, and Stonebrook neighborhoods, while avoiding Old Town, Northwest Ames, and the Iowa Department of Transportation and Railroad. 

2 Story houses built post 1946 have the highest correlation with sale price, while single story homes built before the war seem to have the lowest. 

Low density residential zones have the largest range of prices, but 

## Model conclusion and future applications

Despite the relatively unstable model, key valuable features still revealed themselves.
The model could be applied to other cities in certain regards, but falls short when considering the particularity of some of the location features.
The prominence of certain features in our model may be diminished or pronounced in different cities given the unique nature of its college town status. (ie, bedroom count, location, recession-proof)
