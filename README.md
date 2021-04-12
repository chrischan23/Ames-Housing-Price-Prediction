## Ames Housing Data - Predictive Modelling 

## Contents

- [Problem Statement](#Problem-Statement)
- [Executive Summary](#Executive-Summary)
- [Contents of Notebooks](#Contents-of-Notebooks)
- [Data Dictionary](#Data-Dictionary)
- [Conclusions and Recommendations](#Conclusions-and-Recommendations)
- [Sources](#Sources)


## Problem Statement
For home owners, real estate companies and real estate investors alike, often spend large amounts of money remodeling a home is hoping to earn a profit in return. According to the 2019 Remodeling Impact Report by the National Association of Realtors® Research Group, U.S. homeowners spend more than $400 billion each year on renovations and repairs. Most of which are unable to achieve their ideal return on investment. They either overspend on renovations or focus their remodelling and renovation work on the wrong features of the house, thus making losses rather than profits.

Hence we will try to solve this problem by building a model that predicts housing prices based on different distinct features of a home. We will analyzing housing data from the Ames, Iowa to:
* predict housing targets from their actual sale price
* find what are the features that affect house prices the most

## Executive Summary

We will first import two data sets, train and test, of the Ames Housing Dataset. We will create a model based on the train dataset with sale price as our target.After which, use the test dataset(unseen data) to see how accurate our model is.

After importing both data sets, we will clean the data to ensure that it can be used accurately for our model. Things to look out for is completeness(ie if there are any missing or null data and how to treat them). Also are the data in the correct data types and if the values in each column makes sense. 

Next, we will do a Exploratory Data Analysis(EDA) to analyze and indentify any correlation and trends of house features with sale price. We do this by plotting correlation heat maps, box plots, scatter plots and historgrams. This will give us a first indication of the features that we want to focus on.

For the preprocessing stage we will convert categorical data into numerical data to allow us to examine the data on the same scale. For nominal data, we will use Dummy Variable Encoding. Ordinal data variables will be mapped to a numerical rating in terms of order. Ideally a low number for a lower grade/quality and a larger number for a higher grade/quality.

Before we start to run a our model, we will remove outliers identified in order to prevent distortion of results. Next we have to ensure that there are same number of columns for our train and test dataset.

We will do a train/test split on our dataset in other to determine how well our model works for seen and unseen data. 
Because scales of our datasets are different, we will fit all variables in a standard scaler to standardise all attributes to the same scale. We will then use the linear regression as our baseline model.

After which we will perform a cross validation of Lasso, Ridge, ElasticNet to compare scores so that we can identify the model which performs the best for the Ames Housing data. We will further analyze each model by finding searching for the optimised hyperparameters that will provide the best results for our models to work with. We analyze the bias and variance of each model and finally, provide recommendations of the best features to focus on to improve sales price of a house. 

## Contents of Notebooks

- [Data_Cleaning Train Numerical Data](code/01a_data_cleaning_train_numerical_data.ipynb)
- [Importing and Cleaning of Test Numerical Data](code/01b_data_cleaning_test_numerical_data.ipynb)
- [Exploratory Data Analysis - Numerical Features](code/02_eda.ipynb)
- [Data Cleaning of Categorical Data](code/03_data_cleaning_categorical_data.ipynb)
- [Model](code/04_model.ipynb)


## Data Dictionary
| Feature         | Type    | Category   | Dataset    | Description                                                                         |
|:-----------------|:---------|:------------|:------------|:-------------------------------------------------------------------------------------|
| PID             | int64   | Nominal    | Train/Test |  Parcel identification number  - can be used with city web site for parcel review.  |
| MS SubClass     | int64   | Nominal    | Train/Test |  Identifies the type of dwelling involved in the sale.                              |
| MS Zoning       | object  | Nominal    | Train/Test |  Identifies the general zoning classification of the sale.                          |
| Lot Frontage    | float64 | Continuous | Train/Test |  Linear feet of street connected to property                                        |
| Lot Area        | int64   | Continuous | Train/Test |  Lot size in square feet                                                            |
| Street          | object  | Nominal    | Train/Test |  Type of road access to property                                                    |
| Alley           | object  | Nominal    | Train/Test |  Type of alley access to property                                                   |
| Lot Shape       | object  | Ordinal    | Train/Test |  General shape of property                                                          |
| Land Contour    | object  | Nominal    | Train/Test |  Flatness of the property                                                           |
| Utilities       | object  | Ordinal    | Train/Test |  Type of utilities available                                                        |
| Lot Config      | object  | Nominal    | Train/Test |  Lot configuration                                                                  |
| Land Slope      | object  | Ordinal    | Train/Test |  Slope of property                                                                  |
| Neighborhood    | object  | Nominal    | Train/Test |  Physical locations within Ames city limits (map available)                         |
| Condition 1     | object  | Nominal    | Train/Test |  Proximity to various conditions                                                    |
| Condition 2     | object  | Nominal    | Train/Test |  Proximity to various conditions (if more than one is present)                      |
| Bldg Type       | object  | Nominal    | Train/Test |  Type of dwelling                                                                   |
| House Style     | object  | Nominal    | Train/Test |  Style of dwelling                                                                  |
| Overall Qual    | int64   | Ordinal    | Train/Test |  Rates the overall material and finish of the house                                 |
| Overall Cond    | int64   | Ordinal    | Train/Test |  Rates the overall condition of the house                                           |
| Year Built      | int64   | Discrete   | Train/Test |  Original construction date                                                         |
| Year Remod/Add  | int64   | Discrete   | Train/Test |  Remodel date (same as construction date if no remodeling or additions)             |
| Roof Style      | object  | Nominal    | Train/Test |  Type of roof                                                                       |
| Roof Matl       | object  | Nominal    | Train/Test |  Roof material                                                                      |
| Exterior 1st    | object  | Nominal    | Train/Test |  Exterior covering on house                                                         |
| Exterior 2nd    | object  | Nominal    | Train/Test |  Exterior covering on house (if more than one material)                             |
| Mas Vnr Type    | object  | Nominal    | Train/Test |  Masonry veneer type                                                                |
| Mas Vnr Area    | float64 | Continuous | Train/Test |  Masonry veneer area in square feet                                                 |
| Exter Qual      | object  | Ordinal    | Train/Test |  Evaluates the quality of the material on the exterior                              |
| Exter Cond      | object  | Ordinal    | Train/Test |  Evaluates the present condition of the material on the exterior                    |
| Foundation      | object  | Nominal    | Train/Test |  Type of foundation                                                                 |
| Bsmt Qual       | object  | Ordinal    | Train/Test |  Evaluates the height of the basement                                               |
| Bsmt Cond       | object  | Ordinal    | Train/Test |  Evaluates the general condition of the basement                                    |
| Bsmt Exposure   | object  | Ordinal    | Train/Test |  Refers to walkout or garden level walls                                            |
| BsmtFin Type 1  | object  | Ordinal    | Train/Test |  Rating of basement finished area                                                   |
| BsmtFin SF 1    | float64 | Continuous | Train/Test |  Type 1 finished square feet                                                        |
| BsmtFin Type 2  | object  | Continuous | Train/Test |  Rating of basement finished area (if multiple types)                               |
| BsmtFin SF 2    | float64 | Continuous | Train/Test |  Type 2 finished square feet                                                        |
| Bsmt Unf SF     | float64 | Continuous | Train/Test |  Unfinished square feet of basement area                                            |
| Total Bsmt SF   | float64 | Continuous | Train/Test |  Total square feet of basement area                                                 |
| Heating         | object  | Nominal    | Train/Test |  Type of heating                                                                    |
| Heating QC      | object  | Ordinal    | Train/Test |  Heating quality and condition                                                      |
| Central Air     | object  | Nominal    | Train/Test |  Central air conditioning                                                           |
| Electrical      | object  | Ordinal    | Train/Test |  Electrical system                                                                  |
| 1st Flr SF      | int64   | Continuous | Train/Test |  First Floor square feet                                                            |
| 2nd Flr SF      | int64   | Continuous | Train/Test |  Second floor square feet                                                           |
| Low Qual Fin SF | int64   | Continuous | Train/Test |  Low quality finished square feet (all floors)                                      |
| Gr Liv Area     | int64   | Continuous | Train/Test |  Above grade (ground) living area square feet                                       |
| Bsmt Full Bath  | float64 | Discrete   | Train/Test |  Basement full bathrooms                                                            |
| Bsmt Half Bath  | float64 | Discrete   | Train/Test |  Basement half bathrooms                                                            |
| Full Bath       | int64   | Discrete   | Train/Test |  Full bathrooms above grade                                                         |
| Half Bath       | int64   | Discrete   | Train/Test |  Half baths above grade                                                             |
| Bedroom AbvGr   | int64   | Discrete   | Train/Test |  Bedrooms above grade (does NOT include basement bedrooms)                          |
| Kitchen AbvGr   | int64   | Discrete   | Train/Test |  Kitchens above grade                                                               |
| Kitchen Qual    | object  | Ordinal    | Train/Test |  Kitchen quality                                                                    |
| TotRms AbvGrd   | int64   | Discrete   | Train/Test |  Total rooms above grade (does not include bathrooms)                               |
| Functional      | object  | Ordinal    | Train/Test |  Home functionality (Assume typical unless deductions are warranted)                |
| Fireplaces      | int64   | Discrete   | Train/Test |  Number of fireplaces                                                               |
| Fireplace Qu    | object  | Ordinal    | Train/Test |  Fireplace quality                                                                  |
| Garage Type     | object  | Nominal    | Train/Test |  Garage location                                                                    |
| Garage Yr Blt   | float64 | Discrete   | Train/Test |  Year garage was built                                                              |
| Garage Finish   | object  | Ordinal    | Train/Test |  Interior finish of the garage                                                      |
| Garage Cars     | float64 | Discrete   | Train/Test |  Size of garage in car capacity                                                     |
| Garage Area     | float64 | Continuous | Train/Test |  Size of garage in square feet                                                      |
| Garage Qual     | object  | Ordinal    | Train/Test |  Garage quality                                                                     |
| Garage Cond     | object  | Ordinal    | Train/Test |  Garage condition                                                                   |
| Paved Drive     | object  | Ordinal    | Train/Test |  Paved driveway                                                                     |
| Wood Deck SF    | int64   | Continuous | Train/Test |  Wood deck area in square feet                                                      |
| Open Porch SF   | int64   | Continuous | Train/Test |  Open porch area in square feet                                                     |
| Enclosed Porch  | int64   | Continuous | Train/Test |  Enclosed porch area in square feet                                                 |
| 3Ssn Porch      | int64   | Continuous | Train/Test |  Three season porch area in square feet                                             |
| Screen Porch    | int64   | Continuous | Train/Test |  Screen porch area in square feet                                                   |
| Pool Area       | int64   | Continuous | Train/Test |  Pool area in square feet                                                           |
| Pool QC         | object  | Ordinal    | Train/Test |  Pool quality                                                                       |
| Fence           | object  | Ordinal    | Train/Test |  Fence quality                                                                      |
| Misc Feature    | object  | Nominal    | Train/Test |  Miscellaneous feature not covered in other categories                              |
| Misc Val        | int64   | Continuous | Train/Test |  $Value of miscellaneous feature                                                    |
| Mo Sold         | int64   | Discrete   | Train/Test |  Month Sold (MM)                                                                    |
| Yr Sold         | int64   | Discrete   | Train/Test |  Year Sold (YYYY)                                                                   |
| Sale Type       | object  | Nominal    | Train/Test |  Type of sale                                                                       |
| SalePrice       | int64   | Continuous | Train |  Sale price $$                                                                      |


## Conclusions and Recommendations

#### Recommendations

We identify the best and worst features of house as being:

* Top 10
  * Gr Liv Area
  * Overall Qual
  * BsmtFin SF 1
  * Total Bsmt SF
  * Neighborhood_NridgHt
  * Year Built	
  * Exter Qual
  * Neighborhood_StoneBr
  * Sale Type_New
  * Kitchen Qual
 
  
Despite the limitations of missing data and outliers, the model was able to perform feature selection to provide us with the best 10 features which are mainly, area of a house, its quality, age of the house and the neighbourhood. No doubt it is logical that the size of a house with better quality would command a higher price and this model emphasizes that point. Hence if a homebuyer would have to priortise these 2 factors when they are planning their renovations plans. Hence this model can be applicable for not just the city of Ames, but any other cities in America. 

Location is also a factor with houses in the neighbourhoods of Northridge Heights and Stone Brook commanding higher price than other neighborhoods. These 2 neighbourhoods also happen to lie within 2 miles of the famed Iowa State University where it is not only a prestigious university in America, but also the top employer in the city of [Ames](https://en.wikipedia.org/wiki/Ames,_Iowa).   


##### Limitations

Predictions from our model could potentiall have been affected by missing values. Using logical imputation and using numerical imputation like mean, mode and median may be fast and cheap, but it definitely is not the best method in terms of accuracy. 

There is also multicollinearity within the data. For example, Overall Quality is has a high correlation to other features that is attributed to quality like kitchen and basement quality. Model will be more accurate and robust if features are to a large degree, independent with each other. 

There are many outliers still within the dataset that could cause distortion of results, these outliers maybe valid as well as they could be sold as at exorbitantly high prices on rare occasions. Hence the judgement of whether to keep or remove them is important. 

* Other Considerations to Explore:
  * Timing of a sale as interest rates affect housing price too, followed by supply and demand
  * Quality of a house is subjective to the potential house buyer
  * Upcoming infrastructure like roads and public transport may affect house prices too
  * Creating interaction terms among features might generate interesting findings. 
  
##### Sources 
"Is Your Renovation Actually Worth It?" - Brett Martin (https://www.housebeautiful.com/home-remodeling/renovation/a21970155/renovation-worth-the-cost/)

Home renovations that are worth the cost (and the ones that aren't) - CNN Business (https://edition.cnn.com/2020/01/20/success/home-renovations-roi/index.html)