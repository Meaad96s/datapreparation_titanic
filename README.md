# Data Preparation for Titanic Dataset
This lab is about data preparation. Using IBM Data Refinery for shaping operations clean, organize, fix, and validate data.

## Summary

In the life-cycle of Data Science, data preparation is one of the most important stages. Data scientists spend 80% of their time cleansing, shaping and formatting data before doing any analysis. IBM Data Refinery, an intuitive cloud-based data preparation service, where you can quickly source, shape and share your data sets.

## Included Components

* **IBM Watson Studio:** Analyze data using RStudio, Jupyter and Machine Learning Flow in a configured, collaborative environment that includes IBM value-adds, such as managed Spark.

* **IBM Cloud Object Storage:** An IBM Cloud service that provides an unstructured cloud data store to build and deliver cost effective apps and services with high reliability and fast speed to market. This code pattern uses Cloud Object Storage.

* **IBM Data Refinery:** A part of the Watson Data Platform integrated environment and is a self-service data preparation client for data scientists, data engineers, and business analysts. It can transform large amounts of raw data into consumable, quality information that’s ready for analytics. IBM Data Refinery makes it easy to explore, prepare, and deliver data.

## Pre-requisites

* **IBM Cloud account:**  An account must exist to use the platform.
* **Watson Studio service instance:** A service instance must exist to be able use **IBM Data Refinery**.

## Steps
### Create an IBM cloud account
If you do not have an IBM Cloud account, please create an account [here](https://ibm.biz/BdYpAy)
- A lite account, which is a free of charge. Make sure to set the region to US South.

### Create a Watson Studio service instance
If you don't have a **watson Studio** instance, please do the following:
1.Select Catalog found at the top right of the page.
2.Click on Watson from the menu on the left, which you can find under Platform services.
3.Select Browse Services under **Watson Services**.
4.Choose **watson Studio** instance
<p align="center"><img width="947" alt="untitled" src="https://user-images.githubusercontent.com/20974667/47021511-4509b900-d164-11e8-82e4-e13475ba4dbf.png">
 
* Once the main page of the service appears, click on Get Started. This will redirect the browser to the Watson Studio platform. It might ask to confirm IBM Cloud organization and space information.

### Create a Complete Project in Watson Studio
Select **Refine Data** in the get started page. A prompt box will ask to create a project if you previously don't have one.

![](https://user-images.githubusercontent.com/20974667/47075480-5060f100-d205-11e8-963f-e0dbc2917e6a.png)

* Make sure a cloud storage instance exists, or add a new **IBM Cloud Object Storage** instance by clicking on Add under Select storage service.

### Upload Dataset
The operations will be done using Titanic dataset which can be downloaded from ![here](https://github.com/Meaad96s/datapreparation_titanic/blob/master/Titanic_Dataset.zip)

Under the **Asset** tab in the project, choose this icon <img width="39" alt="dataicon" src="https://user-images.githubusercontent.com/20974667/47075498-5b1b8600-d205-11e8-957c-10fa11498354.PNG"> on the right to upload the dataset to the platform.
* Click browse to navigate your folders where the dataset set can be found.
* After it's uploaded, it will be listed in the **Data asset**.

### Open Data Refinery
To start the process, press the triple dots in the right side of the **train.csv** bar to open **Refine**.

![](https://user-images.githubusercontent.com/20974667/47076141-b8640700-d206-11e8-8423-e7eb74018558.png)

### Convert Column Type

All the columns initially are of type string, for better shaping, convert those integer values columns from string to integer.
From the triple dot menu that appears in the right side of each column, select **Convert Column type** and choose the type.
In Titanic's use case, the columns that are converted to **integer** are Survived, PClass, Sibsp and Parch.
The columns are converted to **decimanl** are Age and Fare.
![](https://user-images.githubusercontent.com/20974667/47091437-8dd97480-d22d-11e8-9d71-42991bfa8f50.png)


## missing values

The columns that have missing values in Titanic dataset are Age, Cabin and Embarked.
The method to fulfill the missing values is by calculating the mean of the column values and placing it in the null values.
Under the menu of each intended column, select calculate
 
 ## outliers 
 
 ## duplicates

# Links
[Data Refinery](https://dataplatform.cloud.ibm.com/docs/content/refinery/refining_data.html?context=analytics&linkInPage=true)

# License
[Apache 2.0](https://github.com/Meaad96s/datacleaning_episode2/blob/master/LICENSE)
