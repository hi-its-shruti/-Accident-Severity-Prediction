
Business Problem & Target Audience:
This prediction model will use sample data of car collisions/accidents from a city and use the same to predict accident severity based on factors from the sample data such as light condition, weather condition and road condition.This prediction model will help goverment authority responsible to road transport safety to derive insight and send alerts through SMS and safety boards on road where based on these fearures chances of severe accidents is high.

Description of Data:
Sample data is of accident information. It provides accident severity along with several features including address type, junction type ,light condition, weather condition and road condition etc associated with the accident record. We will use these features and check if prediction model for accident severity can be built based on these features to help  government autority to take measure to avoid the severe accidents.
Severity of accident is what we will try to build a prediction model for based on the features. Below is the description of the data that we will leverage in the project for building the model:
SEVERITYCODE- Injury Collision, Property Damage are the two categories.
ADDRTYPE - Collision address type:
            • Alley
            • Block
            • Intersection
WEATHER- A description of the weather conditions during the time of the collision
ROADCOND- The condition of the road during the collision
LIGHTCOND - The light conditions during the collision. 

The dataset used in this project is provided at the link is: https://s3.us.cloud-object-storage.appdomain.cloud/cf-courses-data/CognitiveClass/DP0701EN/version-2/Data-Collisions.csv

Methodology Used:
>> Data Cleaning
We have only used factors mentioned in Data section, which are SEVERITYCODE, ADDRTYPE, WEATHER, ROADCOND and LIGHTCOND in our predection model. Therefore rest of the columns have been dropped.

>> Convert Data Type
Check the types of the data in interested features. ADDRTYPE, WEATHER, ROADCOND and LIGHTCOND text values are converted to category codes for each. We had categorical data that was of type 'object'. This is not a data type that we could have fed through an algoritim, so label encoding was used to created new classes that were of type int8; a numerical data type.


Prediction Model:
K Means and Logistic regression models have been used to derive prediction model for accident severity. Both the models' accuracy and precision have been checked and found that using logistic regression a good prediction model for accident severity based on features- light condition, weather condition and road condition can be built.
For train/test split, we used 70% of the data for training and 25% of the data for testing.For logistic regression, we used the LogisticRegression() function from sklearn.linear_model to train the model, the C value is set to 1 and the solver is set to ‘liblinear’

Results :
Using logictic regression model accident severity has been derived with 69.9% accuracy.Vased on historical data from weather conditions pointing to certain classes, we can conclude that particular weather conditions have a somewhat impact on whether or not travel could result in property damage (class 1) or injury (class 2).
