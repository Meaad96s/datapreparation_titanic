# Data Preparation for Titanic Dataset
This lab is about data preparation. Using IBM Data Refinery for shaping operations clean, organize, fix, and validate data.

## Summary

In the life-cycle of Data Science, data preparation is one of the most important stages. Data scientists spend 80% of their time cleansing, shaping and formatting data before doing any analysis. IBM Data Refinery, an intuitive cloud-based data preparation service, where you can quickly source, shape and share your data sets. This lab is about 7 minutes long; it will introduce you to **IBM Data Refinery**'s capabilities and how can you utilize it to prepare your data.

The use-case of this lab is Titanic data set. It has 12 columns of type integer, double and string. Some columns need shaping or cleaning operarions to make use of the data to the full extent. Mostly we will fill missing values with different approaches. The lab takes approximately 10 minutes.

## Included Components

* **IBM Watson Studio:** Analyze data using RStudio, Jupyter and Machine Learning Flow in a configured, collaborative environment that includes IBM value-adds, such as managed Spark.

* **IBM Cloud Object Storage:** An IBM Cloud service that provides an unstructured cloud data store to build and deliver cost effective apps and services with high reliability and fast speed to market. This code pattern uses Cloud Object Storage.

* **IBM Data Refinery:** A part of the Watson Data Platform integrated environment and is a self-service data preparation client for data scientists, data engineers, and business analysts. It can transform large amounts of raw data into consumable, quality information that’s ready for analytics. IBM Data Refinery makes it easy to explore, prepare, and deliver data.

## Pre-requisites

* **IBM Cloud account:**  An account must exist to use the platform.
* **Watson Studio service instance:** A service instance must exist to be able use **IBM Data Refinery**.

## Steps
### Create an IBM cloud account
If you do not have an IBM Cloud account, create an account [here](https://ibm.biz/BdYpAy)
- A Lite account, which is a free of charge. Make sure to set the region to US South.

### Create a Watson Studio service instance
If you don't have a **watson Studio** instance, do the following:

1. Select Catalog found at the top right of the page.
2. Click on Watson from the menu on the left, which you can find under Platform services.
3. Select Browse Services under **Watson Services**.
4. Choose **watson Studio** instance
<p align="center"><img width="947" alt="untitled" src="https://user-images.githubusercontent.com/20974667/48708706-50914980-ec14-11e8-8768-23092ab0b330.png"> 
 
* Once the main page of the service appears, click on Get Started. This will redirect your browser to the Watson Studio platform. It might ask to confirm IBM Cloud organization and space information.

### Create a Standard Project in Watson Studio
From the Get Started page, select **Creat a Project**

![](https://user-images.githubusercontent.com/20974667/48708691-4a9b6880-ec14-11e8-8936-64d0ec4f6b8b.png)

Then Choose a **Standard plan**

![](https://user-images.githubusercontent.com/20974667/48708692-4a9b6880-ec14-11e8-88a6-928cc5646f13.png)

* Make sure a cloud storage instance exists, or add a new **IBM Cloud Object Storage** instance by clicking on Add under Select storage service.

![](https://user-images.githubusercontent.com/20974667/48709557-da421680-ec16-11e8-8c07-c90b29db12e2.png)


### Upload Dataset
The operations will be done using Titanic dataset which can be downloaded from ![here](https://github.com/Meaad96s/datapreparation_titanic/blob/master/titanic.csv), save the csv file to apply the following steps.

Under the **Asset** tab in the project, choose this icon <img width="39" alt="dataicon" src="https://user-images.githubusercontent.com/20974667/47075498-5b1b8600-d205-11e8-957c-10fa11498354.PNG"> on the right to upload the dataset to the platform.
* Click browse to navigate your folders where the dataset set can be found, select file **train.csv**.
* After it's uploaded, it will be listed in the **Data asset**.

![](https://user-images.githubusercontent.com/20974667/48709558-da421680-ec16-11e8-8592-9f96cc9de726.png)

### Open Data Refinery
To start the process, press the Action Menu in the right side of the **train.csv** bar to open **Refine**.

![](https://user-images.githubusercontent.com/20974667/47076141-b8640700-d206-11e8-8423-e7eb74018558.png)

### Convert Column Type

All the columns initially are of type string, for better shaping, convert those integer values columns from string to integer.
From the Actions menu (triple dot) that appears in the right side of each column, select **Convert Column type** and choose the type.
In Titanic's use case, the columns that are converted to **integer** are Survived, PClass, Sibsp and Parch.
The columns are converted to **decimanl** are Age and Fare.
![](https://user-images.githubusercontent.com/20974667/47091437-8dd97480-d22d-11e8-9d71-42991bfa8f50.png)


## missing values

The columns that have missing values in Titanic dataset are Age, Cabin and Embarked.
The methods to fulfill the missing values are different for each attribute depending on the purpose of the attribute.

So, to fill the missing values in **Embarked** attribute, we only fill it with 'S' knwong that the passengers actually embarked at Southampton.


For **Cabin** attribute, since tracing the actual cabin for each passenger is impossible. Handling this attribute by creating additional column that has 1 for a passenger who's cabin exists and 0 if it does not exist. Relating to the accident, known passenger's cabin indicate that they survived. To do that follow the below steps:

* Press the Actions menu in the Cabin column.
* Select **Conditional Replace** under the _Organize_ Category

![](https://user-images.githubusercontent.com/20974667/47149880-8a9dc180-d2dd-11e8-91df-a0842297957d.png)

* Add two conditions in Cabin's column, if value **empty** replace it with 0, if not empty replace with 1.

![](https://user-images.githubusercontent.com/20974667/47149881-8b365800-d2dd-11e8-8c2c-a7b188baccfb.png)

* Choose Cabin column in the option of _Replace any remaining values with

![](https://user-images.githubusercontent.com/20974667/47149882-8b365800-d2dd-11e8-9a94-510c9ef03323.png)


For **age** attribute, calculate the mean of the column values and placing it in the null values.
To replace missing values by the mean of the column, do the following:
1. From the Actions menuu choose **Filter condition**.

![](https://user-images.githubusercontent.com/20974667/47507781-817f9800-d87b-11e8-8985-aa6f603768bb.png)

2. Select _column_ **Age** and **Is not empty** under _operator_ for the Filteration condition.

![](https://user-images.githubusercontent.com/20974667/47507780-80e70180-d87b-11e8-9a4c-0ca3e085e156.png)

3. From the **Operation** Bar, select **Summarize** operator.

![](https://user-images.githubusercontent.com/20974667/47507775-804e6b00-d87b-11e8-9da8-78bff22d0d6e.png)

4. Fill in the operation command the required variables like this Summarize(newVarName=operator(column))
`summarize(newAge= mean(``Age``))`
![](https://user-images.githubusercontent.com/20974667/47507779-80e70180-d87b-11e8-9368-11a260cbbc1b.png)

![](https://user-images.githubusercontent.com/20974667/47507776-80e70180-d87b-11e8-802c-1dc37cfc58ee.png)

5. Copy the geneated value to use after, and undo last two action from the backward arrow above.
Since the filteration and the new summerized value is now useless.

![](https://user-images.githubusercontent.com/20974667/47641516-5a74df00-db77-11e8-9d95-cbabda71f10a.png)

6. Select **Age** column again, from the Actions menu choose **Replace missing values**

![](https://user-images.githubusercontent.com/20974667/47641662-b3dd0e00-db77-11e8-9702-70adea3d79fb.png)

Insert the mean value to be replaced with and press _Apply_ button.
![](https://user-images.githubusercontent.com/20974667/47641669-b8092b80-db77-11e8-9478-0aa572041a60.png)

 ## duplicates

Titanic data set does not have sensitive information that should be unique except for the passenger ID. Simply select the Actions menu in **Passenger Id** column and choose **Remove duplicates**.

![](https://user-images.githubusercontent.com/20974667/47646564-5b147200-db85-11e8-9131-c9c5e934703d.png)


# Links
[Data Refinery](https://dataplatform.cloud.ibm.com/docs/content/refinery/refining_data.html?context=analytics&linkInPage=true)

# License
[Apache 2.0](https://github.com/Meaad96s/datacleaning_episode2/blob/master/LICENSE)
