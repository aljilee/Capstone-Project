# Team GoBlue: Property Return Prediction

The following shows you how to replicate our work of predicting the one year return, three year return, and five year return for properties in the borough of Elmbridge, in the United Kingdom using 4 features: parks, social services, schools, and crimes. Our goal for the project is to predict the return rate of houses in the borough of Elmridge, only considering external factors.

## 1. Downloading data

### Cloning the repository

To get started, clone the repository using the following command:

```git clone https://github.com/aljilee/Capstone-Project.git ```

### Folders in repository:

The repository contains 6 folders, separating the files that are in the repository.

  1. data-raw: Contains the raw datasets that we pulled.

  2. data-cleaned: Contains the datasets that have been cleaned and processed.

  3. final-raw-dataset: Contains our final raw dataset.

  4. final-main-dataset: Contains our final main dataset that we used in our predictive models.

  5. notebooks-cleaning: Contains the notebooks that we used for cleaning. Each notebook contains the location/technique that we pulled the data from, as well as the      steps that we did to clean each dataset.

  6. notebooks-models: Contains the notebooks that we used to create our predictve models. 
One of the notebook "Final Prject - Data Exploration" contains some data explorations and some data visualisation which helped us decide the next steps.
It also includes 2 seperate notebooks for Linear Regression Models; one applied on first data features, and the second was applied on adjusted features which was better than the first attempt.

## 2. Installing required packages

Next, download the required packages that we used in our notebooks.

```pip install -r requirements.txt ```

## 3. Data Acquistion and Cleaning

The folders data-raw and notebooks-cleaning contain all of the files that we used in order to clean our data. We have 4 datasets and notebooks that we used to clean our indepdent variables/features:

  1. Parks
  
      To pull our data for parks, we utilized a geocoding API called Geoapify, pulling the data for a list of all parks in Elmbridge. We then cleaned the data and mapped its latitude and longitude to its corresponding Postal Code, using ```Schools Cleaning.ipynb.```
  
  2. Schools
      
      To pull our data for schools, we scraped data from 
      ```https://www.compare-school-performance.service.gov.uk/schools-by-type step=default&table=schools&region=936&geographic=la&for=primary```, 
      getting all schools in the borough of Elmbridge. We then cleaned the data, to only include its location (latitude and longitude) as well as its rating, and mapped it to its corresponding Postal Code. Afterwards, we integer encoded the school rating, to be able to use it in our regression models.
    
  3. Social Services
  
      To pull our data for social services, we scraped data from ```https://www.cqc.org.uk/search/all```, getting all social services in the borough of Elmbridge. We cleaned the data and kept its location (location and longtiude), as well as the type of service it offered. We then mapped it to its corresponding Postal Code.
  
  4. Crimes
  
     To pull our data for crimes, we scraped data from ```https://data.police.uk/docs/```, getting all documented crimes from all over the UK from 2010 to 2021. To filter the data to only our location of interest, we mapped the latitude and longitude to its corresponding Postal Code, and filtered our crimes data to only show crimes that happened in our location of interest.
  
  
  5. Price data
  
    TBD
    
## 4. Feature Engineering
  
  Due to the results in our initial predictive model, we decided to do feature engineering two ways: on an indivudal property level as well as on a ward level. This was done using the files in final-raw-dataset and notebooks-cleaning, with the final output in final-main-dataset.
  
  1. Property Level:
  
     In our first attempt, we wanted to engineer our features at an individual property level. This meant that for our four features: parks, schools, social services, and crime, for each property sold in a particular year, we would get all parks within 1 KM, schools (depending on type) within 1 - 4 KM, social services within 1 - 4 KM, and crime within (1 KM) of each property. For one year return, we would look at the crime in the previous year. For three year return, we would look at all the different crime in the previous three years and for five year return, we would look at all the crime in the previous five years.
     
     To engineer our features via distance, we compared the distance of the parks, schools, social services, and crime, to our properties using their respective longitude and latitudes. To calculate the distances between the two locations, we utilized a Python library called geopy. The function ``geopy.distance.geodesic()``
accepts two pairs of coorindates, and returns the distance as KM. We calculated the distance between all parks to all properties, all schools to all properties, etc. and did a count of the number of parks, schools, etc. that met the aforementioned distance threshold that we had set.
    
  2. Ward Level:
    
      In our second attempt, we wanted to engineer our features at a ward level. This meant that for our four features, we would look at all the parks in a particular ward, schools in a particular ward, social services in a particular ward, and crime in a particular ward (following the same year pattern). For example, if we were looking at a property in ward X, the features that we would use for that entry would be all the schools in ward X, all of the social services in ward X, all the crimes in ward X, etc. 
      
      To engineer our features, because we had already mapped all of our features to their respective wards, we created our features by doing a count for the number of schools, parks, social services, and crimes, that were in the same ward as the property. For example, two properties that are in the same ward would have the same features for schools, parks, and social services. The crime data may differ depending on when the house was sold.
   
## Modeling

TBD

# Findings 

TBD

# Conclusion


