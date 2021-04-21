
# Module 2 Final Project


## Introduction

Module 2 has allowed me to build upon my supervised learning techniques and predictive modeling using multivariable regressions. This project will focus on predicting home sale prices based different home attributes, both categorical and continuous. I begin my analysis by munging the provided home sales data. I then attempt to choose the best predictors from a large list of variables. Using my set of predictors, I train a multivariate regression model which I subsequently use to predict the value of a home for a potential buyer. Given the predicted home price based on available market data, the buyer can then decide if the home is overvalued or undervalued.


## The Dataset

The King County dataset is a list of homes sold between May 2014 and May 2015 in King County, Washington State (inclusive of Seattle). The dataset lists 21597 homes with 20 different home attributes (excluding price). Home attributes include the following: 

id - unique identified for a house
dateDate - house was sold
pricePrice - is prediction target
bedroomsNumber - of Bedrooms/House
bathroomsNumber - of bathrooms/bedrooms
sqft_livingsquare - footage of the home
sqft_lotsquare - footage of the lot
floorsTotal - floors (levels) in house
waterfront - House which has a view to a waterfront (0,1,nan)
view - Has been viewed (0-4, nan)
condition - How good the condition is ( Overall ) (1-5)
grade - overall grade given to the housing unit, based on King County grading system (3-13)
sqft_above - square footage of house apart from basement
sqft_basement - square footage of the basement
yr_built - Built Year
yr_renovated - Year when house was renovated
zipcode - zip
lat - Latitude coordinate
long - Longitude coordinate
sqft_living15 - The square footage of interior housing living space for the nearest 15 neighbors
sqft_lot15 - The square footage of the land lots of the nearest 15 neighbors


Unfortunately, 63 homes do not have view information, 2376 do not have waterfront information and 3842 do not have renovation information.
This makes up 0%, 11% and 18% of total homes respectively. Given their low percentages compared to the total number of homes in the set, I chose to exclude these specific homes. 

In addition, the range of home prices varied drastically, making predicting home values difficult. I therefore chose to eliminate the upper 10% of homes and focused on middle priced properties. 

The dataset provided both latitude and longitude data. According to zipdatamaps.com, the most expensive zipcode in King County is 98039 (Medina). I therefore calculated the distance of each home from Medina County using latitude and longitude data points and thus creating a single variable rather than two. 

Research has shown that new construction homes and newly rennovated homes can require a premium. I therefore used renovation date and build date to find homes that were upgraded in the last 5 years. Therefore turning both variables into categorical data. 

I also converted basement square footage to a categorical variable to include whether a home had a basement or not since the majoriy of homes listed did not. 


Looking at the correlation between continuous variables revealed that that sqft_above and living are highly correlated however sqft_lot and living are not highly correlated. Whereas baths and beds are highly correlated (88%). I therefore removed sqft_above variable and calculated which categorical variable had a better relationship with price by running a linear regression. Baths had a greater relationship with price compared to bedrooms as shown by their adjusted R squareds of .14 and .07 respectively. I therefore removed the bedroom variable from my dataset.

## Standarization

I logged and standardized each continuous variable to negate any magnitude effects and reduce skewness. I then created dummy variables (binomials) for all of the categorical attributes. Doing so resulted in a final count of 32 potential variables for my regression model.

## Methods

In order to choose the correct variables for my regression model, I ran a best subsets function using Mallow's Cp, AIC, BIC, and Rsquared to determine which variables contributed the largest impact to the regression without reducing explanatory power. Mallow's Cp resulted in 25 variables of the 32, while BICs resulted in 22 and adjusted Rsquared resulted in 26 variables. I decided to go with the 25 variables. 

Using the selected variables, I created both a train and test set from the 14,185 property dataset. I then trained a regression model on the train set and tested on the test. This resulted in a Train MSE of 9611489617.752848 and a Test MSE of 9949479917.362352. I also attempted the K-Folds method with 10 folds to calculate a MSE of 9757804158.897976. The K-Folds MSE equates to a price error of $98,781 in my model which I was happy with. 

## Conclusion

Using my completed multivariable regression model, I predicted the home value of a specific home that a potential buyer was interested in. The home was close in proximity to Medina County (14.821 sq miles),  3 bed, 4 bath, 3,481 sqft livable space, built in 2006, with a 16,988 sqft lot, gorgeous views of the water, and highly rated. By plugging these attributes into my regression formula, I was able to predict a home value of $927404.08. On zillow, this specific home was pricing for $899,900. Based on the model, this home is undervalued and would be a good option for the buyer to place a bid on. 

