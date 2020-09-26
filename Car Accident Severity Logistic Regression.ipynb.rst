.. code:: ipython3

    import numpy as np
    import pandas as pd
    import random as rnd
    import time
    from matplotlib import pyplot as plt
    import seaborn as sns

.. code:: ipython3

    rdd_accidents = pd.read_excel(r'C:\Users\SHRUTICHANDRA\Downloads\Data-Collisions.xlsx')

.. code:: ipython3

    rdd_accidents.head()




.. raw:: html

    <div>
    <style scoped>
        .dataframe tbody tr th:only-of-type {
            vertical-align: middle;
        }
    
        .dataframe tbody tr th {
            vertical-align: top;
        }
    
        .dataframe thead th {
            text-align: right;
        }
    </style>
    <table border="1" class="dataframe">
      <thead>
        <tr style="text-align: right;">
          <th></th>
          <th>SEVERITYCODE</th>
          <th>X</th>
          <th>Y</th>
          <th>OBJECTID</th>
          <th>INCKEY</th>
          <th>COLDETKEY</th>
          <th>REPORTNO</th>
          <th>STATUS</th>
          <th>ADDRTYPE</th>
          <th>INTKEY</th>
          <th>...</th>
          <th>ROADCOND</th>
          <th>LIGHTCOND</th>
          <th>PEDROWNOTGRNT</th>
          <th>SDOTCOLNUM</th>
          <th>SPEEDING</th>
          <th>ST_COLCODE</th>
          <th>ST_COLDESC</th>
          <th>SEGLANEKEY</th>
          <th>CROSSWALKKEY</th>
          <th>HITPARKEDCAR</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>0</th>
          <td>2</td>
          <td>-122.323148</td>
          <td>47.703140</td>
          <td>1</td>
          <td>1307</td>
          <td>1307</td>
          <td>3502005</td>
          <td>Matched</td>
          <td>Intersection</td>
          <td>37475.0</td>
          <td>...</td>
          <td>Wet</td>
          <td>Daylight</td>
          <td>NaN</td>
          <td>NaN</td>
          <td>NaN</td>
          <td>10</td>
          <td>Entering at angle</td>
          <td>0</td>
          <td>0</td>
          <td>N</td>
        </tr>
        <tr>
          <th>1</th>
          <td>1</td>
          <td>-122.347294</td>
          <td>47.647172</td>
          <td>2</td>
          <td>52200</td>
          <td>52200</td>
          <td>2607959</td>
          <td>Matched</td>
          <td>Block</td>
          <td>NaN</td>
          <td>...</td>
          <td>Wet</td>
          <td>Dark - Street Lights On</td>
          <td>NaN</td>
          <td>6354039.0</td>
          <td>NaN</td>
          <td>11</td>
          <td>From same direction - both going straight - bo...</td>
          <td>0</td>
          <td>0</td>
          <td>N</td>
        </tr>
        <tr>
          <th>2</th>
          <td>1</td>
          <td>-122.334540</td>
          <td>47.607871</td>
          <td>3</td>
          <td>26700</td>
          <td>26700</td>
          <td>1482393</td>
          <td>Matched</td>
          <td>Block</td>
          <td>NaN</td>
          <td>...</td>
          <td>Dry</td>
          <td>Daylight</td>
          <td>NaN</td>
          <td>4323031.0</td>
          <td>NaN</td>
          <td>32</td>
          <td>One parked--one moving</td>
          <td>0</td>
          <td>0</td>
          <td>N</td>
        </tr>
        <tr>
          <th>3</th>
          <td>1</td>
          <td>-122.334803</td>
          <td>47.604803</td>
          <td>4</td>
          <td>1144</td>
          <td>1144</td>
          <td>3503937</td>
          <td>Matched</td>
          <td>Block</td>
          <td>NaN</td>
          <td>...</td>
          <td>Dry</td>
          <td>Daylight</td>
          <td>NaN</td>
          <td>NaN</td>
          <td>NaN</td>
          <td>23</td>
          <td>From same direction - all others</td>
          <td>0</td>
          <td>0</td>
          <td>N</td>
        </tr>
        <tr>
          <th>4</th>
          <td>2</td>
          <td>-122.306426</td>
          <td>47.545739</td>
          <td>5</td>
          <td>17700</td>
          <td>17700</td>
          <td>1807429</td>
          <td>Matched</td>
          <td>Intersection</td>
          <td>34387.0</td>
          <td>...</td>
          <td>Wet</td>
          <td>Daylight</td>
          <td>NaN</td>
          <td>4028032.0</td>
          <td>NaN</td>
          <td>10</td>
          <td>Entering at angle</td>
          <td>0</td>
          <td>0</td>
          <td>N</td>
        </tr>
      </tbody>
    </table>
    <p>5 rows × 38 columns</p>
    </div>



.. code:: ipython3

    rdd_accidents.drop(['OBJECTID', 'COLDETKEY','REPORTNO','INTKEY','EXCEPTRSNCODE','EXCEPTRSNDESC','INATTENTIONIND','UNDERINFL','PEDROWNOTGRNT','SEGLANEKEY','CROSSWALKKEY'],axis=1,inplace = True)
    
    rdd_accidents.drop(['SEVERITYCODE.1', 'SEVERITYDESC','COLLISIONTYPE','SDOT_COLDESC'],axis=1,inplace = True)
    
    rdd_accidents.drop(['HITPARKEDCAR', 'ST_COLDESC','SPEEDING','SDOTCOLNUM'],axis=1,inplace = True)
    rdd_accidents.drop(['STATUS', 'LOCATION','INCDATE'],axis=1,inplace = True)
    rdd_accidents.drop(['PERSONCOUNT', 'PEDCOUNT','PEDCYLCOUNT','VEHCOUNT'],axis=1,inplace = True)
    
    rdd_accidents.head(5)
    




.. raw:: html

    <div>
    <style scoped>
        .dataframe tbody tr th:only-of-type {
            vertical-align: middle;
        }
    
        .dataframe tbody tr th {
            vertical-align: top;
        }
    
        .dataframe thead th {
            text-align: right;
        }
    </style>
    <table border="1" class="dataframe">
      <thead>
        <tr style="text-align: right;">
          <th></th>
          <th>SEVERITYCODE</th>
          <th>X</th>
          <th>Y</th>
          <th>INCKEY</th>
          <th>ADDRTYPE</th>
          <th>INCDTTM</th>
          <th>JUNCTIONTYPE</th>
          <th>SDOT_COLCODE</th>
          <th>WEATHER</th>
          <th>ROADCOND</th>
          <th>LIGHTCOND</th>
          <th>ST_COLCODE</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>0</th>
          <td>2</td>
          <td>-122.323148</td>
          <td>47.703140</td>
          <td>1307</td>
          <td>Intersection</td>
          <td>2013-03-27 14:54:00</td>
          <td>At Intersection (intersection related)</td>
          <td>11</td>
          <td>Overcast</td>
          <td>Wet</td>
          <td>Daylight</td>
          <td>10</td>
        </tr>
        <tr>
          <th>1</th>
          <td>1</td>
          <td>-122.347294</td>
          <td>47.647172</td>
          <td>52200</td>
          <td>Block</td>
          <td>2006-12-20 18:55:00</td>
          <td>Mid-Block (not related to intersection)</td>
          <td>16</td>
          <td>Raining</td>
          <td>Wet</td>
          <td>Dark - Street Lights On</td>
          <td>11</td>
        </tr>
        <tr>
          <th>2</th>
          <td>1</td>
          <td>-122.334540</td>
          <td>47.607871</td>
          <td>26700</td>
          <td>Block</td>
          <td>2004-11-18 10:20:00</td>
          <td>Mid-Block (not related to intersection)</td>
          <td>14</td>
          <td>Overcast</td>
          <td>Dry</td>
          <td>Daylight</td>
          <td>32</td>
        </tr>
        <tr>
          <th>3</th>
          <td>1</td>
          <td>-122.334803</td>
          <td>47.604803</td>
          <td>1144</td>
          <td>Block</td>
          <td>2013-03-29 09:26:00</td>
          <td>Mid-Block (not related to intersection)</td>
          <td>11</td>
          <td>Clear</td>
          <td>Dry</td>
          <td>Daylight</td>
          <td>23</td>
        </tr>
        <tr>
          <th>4</th>
          <td>2</td>
          <td>-122.306426</td>
          <td>47.545739</td>
          <td>17700</td>
          <td>Intersection</td>
          <td>2004-01-28 08:04:00</td>
          <td>At Intersection (intersection related)</td>
          <td>11</td>
          <td>Raining</td>
          <td>Wet</td>
          <td>Daylight</td>
          <td>10</td>
        </tr>
      </tbody>
    </table>
    </div>



.. code:: ipython3

    rdd_accidents.WEATHER = pd.Categorical(rdd_accidents.WEATHER)
    rdd_accidents['WEATHER_CODE'] = rdd_accidents.WEATHER.cat.codes
    
    rdd_accidents.ROADCOND = pd.Categorical(rdd_accidents.ROADCOND)
    rdd_accidents['ROADCOND_CODE'] = rdd_accidents.ROADCOND.cat.codes
    
    rdd_accidents.LIGHTCOND = pd.Categorical(rdd_accidents.LIGHTCOND)
    rdd_accidents['LIGHTCOND_CODE'] = rdd_accidents.LIGHTCOND.cat.codes
    
    
    rdd_accidents.JUNCTIONTYPE = pd.Categorical(rdd_accidents.JUNCTIONTYPE)
    rdd_accidents['JUNCTIONTYPE'] = rdd_accidents.JUNCTIONTYPE.cat.codes
    
    rdd_accidents.ADDRTYPE = pd.Categorical(rdd_accidents.ADDRTYPE)
    rdd_accidents['ADDRTYPE'] = rdd_accidents.ADDRTYPE.cat.codes
    
    rdd_accidents.ADDRTYPE = pd.Categorical(rdd_accidents.ADDRTYPE)
    rdd_accidents['ADDRTYPE'] = rdd_accidents.ADDRTYPE.cat.codes
    
    rdd_accidents.head(5)




.. raw:: html

    <div>
    <style scoped>
        .dataframe tbody tr th:only-of-type {
            vertical-align: middle;
        }
    
        .dataframe tbody tr th {
            vertical-align: top;
        }
    
        .dataframe thead th {
            text-align: right;
        }
    </style>
    <table border="1" class="dataframe">
      <thead>
        <tr style="text-align: right;">
          <th></th>
          <th>SEVERITYCODE</th>
          <th>X</th>
          <th>Y</th>
          <th>INCKEY</th>
          <th>ADDRTYPE</th>
          <th>INCDTTM</th>
          <th>JUNCTIONTYPE</th>
          <th>SDOT_COLCODE</th>
          <th>WEATHER</th>
          <th>ROADCOND</th>
          <th>LIGHTCOND</th>
          <th>ST_COLCODE</th>
          <th>WEATHER_CODE</th>
          <th>ROADCOND_CODE</th>
          <th>LIGHTCOND_CODE</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>0</th>
          <td>2</td>
          <td>-122.323148</td>
          <td>47.703140</td>
          <td>1307</td>
          <td>3</td>
          <td>2013-03-27 14:54:00</td>
          <td>2</td>
          <td>11</td>
          <td>Overcast</td>
          <td>Wet</td>
          <td>Daylight</td>
          <td>10</td>
          <td>4</td>
          <td>8</td>
          <td>5</td>
        </tr>
        <tr>
          <th>1</th>
          <td>1</td>
          <td>-122.347294</td>
          <td>47.647172</td>
          <td>52200</td>
          <td>2</td>
          <td>2006-12-20 18:55:00</td>
          <td>5</td>
          <td>16</td>
          <td>Raining</td>
          <td>Wet</td>
          <td>Dark - Street Lights On</td>
          <td>11</td>
          <td>6</td>
          <td>8</td>
          <td>2</td>
        </tr>
        <tr>
          <th>2</th>
          <td>1</td>
          <td>-122.334540</td>
          <td>47.607871</td>
          <td>26700</td>
          <td>2</td>
          <td>2004-11-18 10:20:00</td>
          <td>5</td>
          <td>14</td>
          <td>Overcast</td>
          <td>Dry</td>
          <td>Daylight</td>
          <td>32</td>
          <td>4</td>
          <td>0</td>
          <td>5</td>
        </tr>
        <tr>
          <th>3</th>
          <td>1</td>
          <td>-122.334803</td>
          <td>47.604803</td>
          <td>1144</td>
          <td>2</td>
          <td>2013-03-29 09:26:00</td>
          <td>5</td>
          <td>11</td>
          <td>Clear</td>
          <td>Dry</td>
          <td>Daylight</td>
          <td>23</td>
          <td>1</td>
          <td>0</td>
          <td>5</td>
        </tr>
        <tr>
          <th>4</th>
          <td>2</td>
          <td>-122.306426</td>
          <td>47.545739</td>
          <td>17700</td>
          <td>3</td>
          <td>2004-01-28 08:04:00</td>
          <td>2</td>
          <td>11</td>
          <td>Raining</td>
          <td>Wet</td>
          <td>Daylight</td>
          <td>10</td>
          <td>6</td>
          <td>8</td>
          <td>5</td>
        </tr>
      </tbody>
    </table>
    </div>



.. code:: ipython3

    rdd_accidents.drop(['WEATHER', 'ROADCOND','LIGHTCOND'],axis=1,inplace = True)
    rdd_accidents.drop(['X','Y','ST_COLCODE'],axis=1,inplace = True)
    
    #rdd_accidents.drop(['LIGHTCOND'],axis=1,inplace = True)
    rdd_accidents.head(5)




.. raw:: html

    <div>
    <style scoped>
        .dataframe tbody tr th:only-of-type {
            vertical-align: middle;
        }
    
        .dataframe tbody tr th {
            vertical-align: top;
        }
    
        .dataframe thead th {
            text-align: right;
        }
    </style>
    <table border="1" class="dataframe">
      <thead>
        <tr style="text-align: right;">
          <th></th>
          <th>SEVERITYCODE</th>
          <th>INCKEY</th>
          <th>ADDRTYPE</th>
          <th>INCDTTM</th>
          <th>JUNCTIONTYPE</th>
          <th>SDOT_COLCODE</th>
          <th>WEATHER_CODE</th>
          <th>ROADCOND_CODE</th>
          <th>LIGHTCOND_CODE</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>0</th>
          <td>2</td>
          <td>1307</td>
          <td>3</td>
          <td>2013-03-27 14:54:00</td>
          <td>2</td>
          <td>11</td>
          <td>4</td>
          <td>8</td>
          <td>5</td>
        </tr>
        <tr>
          <th>1</th>
          <td>1</td>
          <td>52200</td>
          <td>2</td>
          <td>2006-12-20 18:55:00</td>
          <td>5</td>
          <td>16</td>
          <td>6</td>
          <td>8</td>
          <td>2</td>
        </tr>
        <tr>
          <th>2</th>
          <td>1</td>
          <td>26700</td>
          <td>2</td>
          <td>2004-11-18 10:20:00</td>
          <td>5</td>
          <td>14</td>
          <td>4</td>
          <td>0</td>
          <td>5</td>
        </tr>
        <tr>
          <th>3</th>
          <td>1</td>
          <td>1144</td>
          <td>2</td>
          <td>2013-03-29 09:26:00</td>
          <td>5</td>
          <td>11</td>
          <td>1</td>
          <td>0</td>
          <td>5</td>
        </tr>
        <tr>
          <th>4</th>
          <td>2</td>
          <td>17700</td>
          <td>3</td>
          <td>2004-01-28 08:04:00</td>
          <td>2</td>
          <td>11</td>
          <td>6</td>
          <td>8</td>
          <td>5</td>
        </tr>
      </tbody>
    </table>
    </div>



.. code:: ipython3

    #split dataset in features and target variable
    feature_cols = ['WEATHER_CODE', 'ROADCOND_CODE', 'LIGHTCOND_CODE','JUNCTIONTYPE','ADDRTYPE']
    X = rdd_accidents[feature_cols] # Features
    y = rdd_accidents.SEVERITYCODE # Target variable

.. code:: ipython3

    from sklearn.model_selection import train_test_split

.. code:: ipython3

    # split X and y into training and testing sets
    from sklearn.model_selection import train_test_split
    X_train,X_test,y_train,y_test=train_test_split(X,y,test_size=0.25,random_state=0)

.. code:: ipython3

    # import the class
    from sklearn.linear_model import LogisticRegression
    
    # instantiate the model (using the default parameters)
    logreg = LogisticRegression()
    
    # fit the model with data
    logreg.fit(X_train,y_train)
    
    #
    y_pred=logreg.predict(X_test)
    
    print(y_pred)
    


.. parsed-literal::

    [1 1 1 ... 1 1 1]
    

.. code:: ipython3

    import sklearn.metrics as metrics
    print("Accuracy:",metrics.accuracy_score(y_test, y_pred))
    print("Precision:",metrics.precision_score(y_test, y_pred))
    print("Recall:",metrics.recall_score(y_test, y_pred))


.. parsed-literal::

    Accuracy: 0.6994390679898909
    Precision: 0.7013392949553914
    Recall: 0.994131627593087
    


