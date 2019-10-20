# Model for apartment selling prices in mainland Queens, NY

## Table of Contents:
+ [Data Set](#Data_Set) </br>
+ [Result](#Results) </br>

## <a name="Data_Set"></a> Data Set 

The raw data were drawn from Multiple Listing Services. The data set was harvested with MTurk and it is a raw download from their website. Mainly zip codes from mainland Queens, leaving out the Rockaways, a peninsula near JFK airport that is geographically distinct from the rest of the neighborhoods, with a total of 55 zipcodes from Queens, NY. Data cleaning was performed in order to improve the dataset.

This dataset partly represents the population of interest because this is a fairly small sample size of Queens. Certain zipcodes have just a few observations in comparison to the other zipcodes that have a larger size of obsevations.
External sources were not use in this project, but featurization was done using the provided dataset. 

There were dangers of extrapolation because the prediction of this data can only predict on the zipcodes within the range provided that have same number of bedrooms, bathrroms, and should not be used to make predictions outside of the range.
For example, this model is predicting for studios, homes that has up to three bedrooms, using the same model to predict home that have over 3 bedrooms would be extrapolation. 

In this dataset there are outliers, for example the house that worth close to $1M or in the total taxes that ranges from $11 to $9300. It does not take account on weird cases, it will predict poorly on them.


There are total 25 features:

**Categorical Features**
- coop_condo: apartments that are either coops or condos 
(Some important fact to keep in mind: coops are those that have more community charges, you don’t own the apartment, however, you own a stock in the cooporation that owns the building. In order to buy coops you have to be approved by the coorperation board. Coops also have less freedom in renting or subletting. Co-ops are also cheaper then condos. In Comparison to co_ops a person actually owns the apartment, and has the freedom to make the changes in the floor plans and almost two times as expensive)
- dining_room_type: this was factorial and was combo, formal or other 
- garage_exists: existence of garage
- kitchen_type: the feature was factorial but we made it into two different kinds “eat in” and “efficeny” or none 
- parking_charges: the charge for the parking space
- total_taxes: the property tax charged by the local government 


**Numerical Features**
- approx_year_built: prewar built would be concrete walls, and brick outside, old elevators and modern ones that are built would be wood 
- community_district_num: determines school districts 
- num_bedrooms: number of bedrooms 
- num_floors_in_building: number of floors
- num_full_bathrooms: number of full bathrooms
- num_half_bathrooms: number of half bathrooms
- num_total_rooms: number of total rooms
- sq_footage: the size of the apartment by square feet 
- walk_score: it is the walk to the nearby stores
- pct_tax_deductibl: the percentage of dedutable taxable income 

Within the 25 features, we created more features from raw data that help facilitate the model making process, such as:

**Featurization**
- pets_allowed: cats_allowed and dog_allowed were combined into one column because they were collinear
- monthly_charges: maintenance_cost and common_charges were combined into one column since they are mutually exclusive 
- price_per_sqft: using listing_price to divide by sqr_footage, then dropping listing_price and sqr_footage 
- lat: latitude of addresses from full_address_or_zip_code. Using the R package, ggmap, to get the coordinates from the given feature full_address_or_zip_code
- lon: longitude of addresses from full_address_or_zip_code. Using the R package, ggmap, to get the coordinates from the given feature full_address_or_zip_code
- distance_to_the_closest_LIRR: using ggmap to get the latitude and longitude of each LIRR station in Queens, then ran a code to find the nearest distance of each coop/condo to the closest LIRR station

**Target Variable**
- sale_price: The target variable. 
***

## <a name="Results"></a> Result

On test set: 
Three different models were used to predict on prices to calculate best outcome of prices.

- Regression Tree Modeling: The were only six variable used for spliting; therefore it was not accurate for prediction on sale prices (The purpose of this model is to show the difference between Regression Trees and Random Forest Modeling)
- Linear Modeling: in sample R^2 = 84 and out of sample R^2 = 85; The RMSE is plus or minus $83215.95
- Random Forest Modeling: in sample R^2 = 84 and out of sample R^2 = 85; The RMSE is plus or minu $70000
