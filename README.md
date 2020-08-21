# Analysis of NYC's Green-Taxi Data
##Introduction
- For this project, we have used **NYC green taxi data**. This data is available in ***JSON*** [(***What is JSON?***)](https://www.json.org/) format.
- Green taxi data is available for year 2009 and year 2014 to 2018. Which is taken from this [**Link**](https://data.cityofnewyork.us/browse?q=green+taxi).
- The data dictionary can be viewed or downloaded from this [**Link**](https://www1.nyc.gov/assets/tlc/downloads/pdf/data_dictionary_trip_records_green.pdf). 
- This project is divided into **three** parts.
	-	Taxi data analysis of different years 
	-	Time series analysis
	-	Applying machine learning models
- **Taxi data analysis of different years:**		
	-	 To know the change in number of short distance trips and long distance trips for different years.
	-	 To know the change in total number of trips over the year.
	-	 To check if there is a change in average fare amount for trip distance between 0 to 10 over the years.
	-	 To know the revenue for each year.
	-	 To know the type of payment method people use over the year. Further we can know if they tend to use different payment method in the past compare to present. 
- **Time series analysis:**
	-	To know in which months people use taxi more. 
	-	To know if weather conditions has any relation with people using taxi.
	-	To know if there is any difference in fare amount for each days of the week. 
	-	To know the time stamps of each pickups and drop-offs for short distance trips and long distance trips. Further we can know if there is any particular time range in which people tend to use taxi more. 
	-	To know the number of passengers for short distance trips and long distance trips. 
- **Applying machine learning models:**
	-	For this part of the project, we've used different machine learning models such as OLS[**(What is OLS?)**](https://en.wikipedia.org/wiki/Ordinary_least_squares), Linear Regression[**(What is Linear Regression?)**](https://en.wikipedia.org/wiki/Linear_regression), Multiple Linear Regression[**(What is Multiple Linear Regression?)**](https://www.investopedia.com/terms/m/mlr.asp), Ridge Regression[**(What is Ridge Regression?)**](https://ncss-wpengine.netdna-ssl.com/wp-content/themes/ncss/pdf/Procedures/NCSS/Ridge_Regression.pdf), Lasso[**(What is Lasso?)**](https://en.wikipedia.org/wiki/Lasso_(statistics)). 
	-	Data has been divided into train data set and test data set. And after building the model, model has been evaluated on the test data set.
	-	Best model has been chosen by considering Root Mean Square Error(RMSE) value[**(What is RMSE?)**](http://statweb.stanford.edu/~susan/courses/s60/split/node60.html).

##Requirements
- There is no requirement of having a unique API key for this data set.
- However to run the given code, you may need to import/download different packages which are listed below. Mostly all these packages are pre-installed in Anaconda. But in rare case, you may need to download few of these packages. To do so, refer to the link given. After going to link, copy the **```pip install```** command for respective package and simply run it thorough anaconda prompt. 
- For example, If we want to download **pandas**,this is the command(**```pip install pandas```**) we get from the link listed below. To download the package, simply write this command in **Anaconda Prompt** and required package will be installed. 

 

	-	json
	-	urllib
	-	pandas [**(Link)**](https://pypi.org/project/pandas/)
	-	numpy [**(Link)**](https://pypi.org/project/numpy/)
	-	matplotlib.pyplot [**(Link)**](https://pypi.org/project/matplotlib/)
	-	seaborn [**(Link)**](https://pypi.org/project/seaborn/)
	-	statistics [**(Link)**](https://pypi.org/project/statistics/)
	-	sklearn [**(Link)**](https://pypi.org/project/scikit-learn/)
	-	math
	-	datetime [**(Link)**](https://pypi.org/project/DateTime/)
	-	statsmodels.api [**(Link)**](https://pypi.org/project/statsmodels/)
	-	random [**(Link)**](https://pypi.org/project/random2/)
	
---

##Explanation of the code and results obtained

##Part1: Taxi data analysis of different years

Before getting started, we need to import few packages.

	#Importing required packages
	import json
	import urllib
	import pandas as pd
	import numpy as np
	import matplotlib.pyplot as plt
	import seaborn as sb
	import statistics

Further, we can begin to load required [**data**](https://data.cityofnewyork.us/browse?q=green+taxi) for each years. 

	#getting data for year 2018
	url1 = 'https://data.cityofnewyork.us/resource/w7fs-fd9i.json?$limit=50000'
	
	#converting to pandas dataframe
	df1 = pd.read_json(url1, orient = 'columns')
	
	#converting to datetime format
	df1['lpep_dropoff_datetime'] = pd.to_datetime(df1['lpep_dropoff_datetime'])
	df1['lpep_pickup_datetime'] = pd.to_datetime(df1['lpep_pickup_datetime'])

	df1['trip_time'] = df1['lpep_dropoff_datetime'] - df1['lpep_pickup_datetime'] #HH:MM:SS
	df1['diff_time']=df1['trip_time']/np.timedelta64(1,'m') #output in minutes
	df1 #checking the data

Here, **url1** is the data for year 2018. By using ```$limit=50000``` we have taken 50,000 data for year 2018. Further this data is converted into pandas dataframe using ```pd.read_json``` and which has been named as ```df1```. 

```trip_time``` is the new column created which has the trip duration information in **HH:MM:SS** format. Further we can convert this information in **minutes only** using this code ```df1['trip_time']/np.timedelta64(1,'m')```. Which is inserted in the dataframe as column name ```diff_time```.

Further we can get the data for the year 2017[(**data**)](https://data.cityofnewyork.us/resource/5gj9-2kzx.json?$limit=50000), 2016[(**data**)](https://data.cityofnewyork.us/resource/pqfs-mqru.json?$limit=50000), 2015 [(**data**)](https://data.cityofnewyork.us/resource/utt9-dvgj.json?$limit=50000), 2014 [(**data**)](https://data.cityofnewyork.us/resource/2np7-5jsg.json?$limit=50000), 2009 [(**data**)](https://data.cityofnewyork.us/resource/f9tw-8p66.json?$limit=50000) as shown above by providing different data. Further we can save the dataframe as ```df2```, ```df3```, ```df4```, ```df5```, ```df6``` respectively.
