# Data-Science-Capstone-Project-Battle-of-Neighbourhoods-Toronto-vs-New-York-City
----
**This project is part of [IBM Data Science Professional Certificate](https://www.coursera.org/professional-certificates/ibm-data-science) and aims to reveal some insights related to property prices and available venues for the people who wants to immigrate to Toronto or  New York City.**

# Problem

---

> **Say, You are planning immigration to either Toronto, Canada or New York City, USA for better life prospects like education, earnings, security and many more. You live in India and love your neighbourhood mainly beacause of all the great amenities and venues that exist in your neighbourhood such as fast food centres, pharmacies, schools, markets, shopping malls, parks, hospitals and so on. You want to know, which city among Toronto and New york city will be economical and similar to your current neighborhood.**

---

# Introduction 

---

## `Objective`
>  This project is targeted to stakeholders interested in immigrating to Toronto, Canada and New York, USA; especially from India as lot's of Indians have been immigrated there in past years and it aims to provide a bird view of variation of housing prices as neighborhood and also the available venues and amenities.
    
## `Libraries used`
**`We will use`**
> * **`pandas`** : for data analysis
> * **`numpy`** : to handle data in a vectorized manner
> * **`json`** : to handle JSON files
> * **`requests`** : to handle requests
> * **`BeautifulSoup`** : for web scrapping
> * **`geopy`** : to convert an address into latitude and longitude values and vice versa
> * **`folium`** : map rendering library
> * **`Matplotlib`** : graph ploting library
> * **`sklearn`** : for kmeans algorithm
> * **`uszipcode`** : for New York Housing Price data
> * **`opendatasets`** : for downloading housing data of Toronto from kaggle
> * **`tqdm`** : TQDM is a progress bar library with good support for nested loops and Jupyter/IPython notebooks
> * **`warnings`** : to remove warnings from outline cell of Jypyter notebook

## `Disclaimer for running this notebook on your platforms`

> * You need a Kaggle account.
> * If you decided to run this notebook, start the auto-pilot for execution of notebook then layback,put your earpods on and enjoy the excution for 30 minutes.

---

## Background

---

**`Why People Immigrate?`**
> Referring to the economic, political, and social influences, people migrate from or to specific countries. Immigrants are motivated to leave their former countries of citizenship, or habitual residence, for a variety of reasons, including: a lack of local access to resources, a desire for economic prosperity, to find or engage in paid work, to better their standard of living, family reunification, retirement, climate or environmentally induced migration, exile, escape from prejudice, conflict or natural disaster, or simply the wish to change one's quality of life.

### `Toronto`

* **`What is Toronto ?`** 
    > Toronto is the capital of the [Canadian province](https://en.wikipedia.org/wiki/Provinces_and_territories_of_Canada) of [Ontario](https://en.wikipedia.org/wiki/Ontario) and the most populous city in Canada, the fourth most populous city in North America. Its current area of 630.2 km2 (243.3 sq mi). [Read more here](https://en.wikipedia.org/wiki/Toronto)

* **`Immigration from India to canada`**
    >[India is the number one source country for immigrants coming from overseas to Canada](https://www.cicnews.com/2020/10/how-to-immigrate-to-canada-from-india-1015949.html#gs.3qjx68) and [The highest concentrations of Indian Canadians are found in the provinces of Ontario](https://en.wikipedia.org/wiki/Indo-Canadians); [followed by the China and the Philippines in 2019](https://www.immigration.ca/where-will-canadas-401000-immigrants-come-from-in-2021).In the five years that ended in 2019, immigration from India, skyrocketed, growing by almost 117.6% from 39,340 in 2015 to 85,590.

* **Explore more about `immigration from different countries to Canada` [here](https://jovian.ai/omprakashp014909/immgration-to-canada-from-1980-to-2013) and `Toronto's Neighborhood` [here](https://jovian.ai/omprakashp014909/exploring-segmenting-and-clustering-neighborhoods-in-the-city-of-toronto-ontario-canada)**

### `New York City(NYC)`

* **`What is New York City?`** 
    > New York City, often simply called New York, is the most populous city distributed over about 784 km2 (302.6 sq mi) in the United States. Located at the southern tip of the State of New York, the city is the center of the New York metropolitan area, the largest metropolitan area in the world by urban area.[Read more here](https://en.wikipedia.org/wiki/New_York_City)


* **`Immigration from India to New York City`**
    >As of 2014-18, the U.S. cities with the largest number of Indians were the greater New York, Chicago, San Francisco, and San Jose metropolitan areas. These four metro areas accounted for about 30 percent of Indians in the United States.[Read more here](https://www.migrationpolicy.org/article/indian-immigrants-united-states-2019)


* **Explore the `Neighborhood of New York City` [here](https://jovian.ai/omprakashp014909/neighborhoods-new-york)**

---

# Data

---
  
* We will need the location data such as postal codes, boroughs, latitude and longitude, housing price data of the neighborhoods of respective cities..

### `1.Location Data`
* **`About data`**
> * For New York City, all the data is available in .csv format on ibm.
> * For Torornto, we will web srape the wikipedia page to grab postal codes, boroughs and neighborhoods and then will merged them with a dataset containing respective latitudes and longitudes.
> * It will be used for segmenting the neighborhoods based on the venues and plot maps for rest of the data.
> * Foursquare REST API will be used to grab the venues in the neighborhood
* **`Sources`**
> * New York City(JSON) : https://cocl.us/new_york_dataset
> * Toronto's Postal Code, Borough and Neighborhoods data : https://en.wikipedia.org/wiki/List_of_postal_codes_of_Canada:_M
> * Toronto's Geospatial data : https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DS0701EN-SkillsNetwork/labs_v1/Geospatial_Coordinates.csv


### `2.Housing Data`
* **`About data`**
> * For New York city, we will use web scrapping to scrape the zip codes from city-data and then use the uszipcode library to grab the housing data for the respective zipcodes. [Read More here](https://uszipcode.readthedocs.io/index.html)
> * For Toronto, the housing dataset is hosted on Kaggle
> * For fair comparison, the prices will be converted to same unit and will be maintained within limit.
* **`Source`**
> * New York City : http://www.city-data.com/zipmaps/New-York-New-York.html
> * Toronto : https://www.kaggle.com/mnabaee/ontarioproperties

## How these data will be used ?
* **`Factors considered`**
> * Venues and amenties available in the neighborhoods of each city. 
> * Housing Price data of each city. 
  
* **`Solution`**
> * We will cluster the neighbourhoods of each city using K Means algorithm in 3 clusters based on Housing Price as Low Budget, Medium Budget and High Budget and based on venues in 10 clusters.
> * Maps will be used for visualization, to know the cluster number of the markers do click on them. Feel free to zoom in and out the maps.

---

# Table of Content

--- 

1. **Install and import the helper libraries**
2. **Load Neighborhood Data**
> * 2.1 Load Neighborhood data of New Delhi, New York City and extract manhattan borough as df_manhattan
> * 2.2 Web Scrape the Neighborhood data of Toronto city and load it's geospatial data and merge both as df_toronto
3. **Visualize the neighborhoods in New York City-Borough Manhattan and City of Toronto**
> * 3.0 Defining functions that will be used for visualization
> * 3.1 Grab coordinates of Boroughs
> * 3.2 Merge df_manhattan and df_toronto
> * 3.3 Visualize where in the world India, Toronto and New city are.
> * 3.4 Visualize neighborhoods of Toronto City and New York City
> * 3.5 Visualize Toronto and Manhattan Bouroughs with Neighborhoods on map
4. **Loading and clustering the Housing Data of New York City and Toronto**
> * 4.1 Loading and data wrangling with the Housing data of New York
> * 4.2 Clustering the Housing Price dataframe for New York
> * 4.3 Loading and data wrangling with the Housing data of Toronto
> * 4.4 Clustering the Housing Price dataframe of Toronto
> * 4.5 Visualize the variation of housing price in the neighborhoods
5. **Import Venue Data of Neighborhoods From Foursquare**
> * 5.1 Load the dataset
> * 5.2 Cluster the dataset into 10 cluster
> * 5.3 Top 10 venues of each neighborhood
> * 5.4 Visualize the neighborhoods as clulster on available venues
> * 5.5 Top 10 venues in each custer
> * 5.6 Number of Neighborhoods in each cluster.
6. **Results and Discusions**
7. **Conclusion**

---

## Methodology
    
> 1. We will load the Borough and Neighborhood data along with the latitudes and longitudes of the neighbourhood. Data for New York will be downloaded from IBM cloud and for Toronto the postalcode,borough and neighborhood data is available on the wikipedia page, we will web scrape from there and after that download it's geospatial data from IBM cloud and merged them in single dataframe followed by the visualization of these data on world map.
> 2. For finding Housing price data of New York, first we will web scrape the zipcodes from city-data and then use the uszipcode lilbrary to load it's housing price data. For Toronto, the dataset is hosted on Kaggle. Once, both the datasets loaded and wrangled, cluster them into three categories as low budget, medium budget and high budget then use it for visualizing the varitiation on world map.
> 3. Use the Folilum's REST API, to load the venes data and cluster the neighbourhood into 10 groups based on similarities in venue then use it for visualilzation.

---
#  Results and Discussions

The New York City populates 306 neighborhoods distributed in 5 boroughs and Toronto being populated by 103 neighborhood distributed in 5 boroughs.

Analysis of Housing Price variation is done by considering the variation in housing price between `$ 76000 - $443888 - $745000 - $1000001` for the neighborhoods as low, medium and high budegt. For accounting variation in currency, currency conversion has been used and an upper and lower bounds has been considered to have similar minimum and maximum prices.
* In New York majority of the houses falled under low budget category followed by medium nad high budget categories. The borough Manhattan is the costliest place to immigrate whereas Bronx being cheapest. Majority of the property in Queens ranges between low budget(majority) to medium budget, on the other hand Brooklyn is categorized as medium budget with few high and low budget properties.Due to restrictions on data availability in uscodelibrary, we were able to get few venues for Staten Island, you can check this by comparing it's number of neighborhoods in 2nd map and number of venues in housing price map.
* On the other hand in Toronto, there were more low budget properties , followed by the medium and high ones with city of Etobicote and Toronto being cotliest. Properties in York ranges between medium to high budget while Scarborough ranging in low to high majority being medium budget.
* As more data was available for toronto, it's classification was more detailed as compared to New York.

Further, total 79 neighborhoods were categorised into 10 clusters based on number and type of venues and amenities available in the neighborhood in which Toronta clusterd into 5 clusters consisting 39 neighborhoods and Manhattan into 7 containing 40 neighborhoods. The venue data had been extracted using REST API calls to Fouesquare database that allows free 950 regular calls and 50 premium calls per day. A table showing top 10 amenities and a tables representing number of neighborhoods for each cluster are also provided for refence. Due to the restriction on number of API calls , only Borough Toronto from Toronto and Borough Manhattan from New York City has been taken into accout.

---

# Conclusion 

Purpose of this project was to identify an affordable property with similarities to present neighborhood in Toronto and New York City in order to aid stakeholders in narrowing down the search for optimal location for immigration. Using property data from uscodelibrary and the dataset from Kaggle, a plot categorizing neighborhoods in low, medium and high budget thereby showing the variation in property prices for 103 neighborhoods of toronto and 306 neghborhoods of New York City has been plotted. Moving further the venue data of each neighbohood has been extracted using API calls from Foursqaure database and this data is clustered into 10 cluster. Also, top 10 venues of each neighborhood and each cluster also generated for comparing the neighborhoods on venues.

Final decission on optimal neighborhood location will be made by stakeholders based on specific characteristics of neighborhoods  , taking into consideration additional factors like attractiveness of each neighborhood (proximity to park or water), crime rate, social and economic dynamics of every neighborhood etc.
