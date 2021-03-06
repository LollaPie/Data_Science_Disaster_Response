# Capstone project: Disaster Response Classification App
## Table of Content
1. [Motivation](#motivation)
2. [Installation](#installation)
3. [About the Data](#about-the-data)
4. [About the Methods](#about-the-methods)
5. [Web Application](#webpage)
6. [Acknowledgements & Licensing](#acknowledgements--licensing)

## Motivation <a name="motivation"/>
Environmental disasters increases due to climate change. Emergency services have a higher impact on disaster responses which they have to classify into categories 
to better process them. Especially during a disaster they have the lowest capacities to process the messages.

As a capstone project for the udacity data science course I build a machine learning model based on python to classifiy these text messages.

## Installation <a name="installation"/>
Python version 3.6 or higher is recommended.

- Clone these repository
- run the 'process_data.py' to clean data and store it in a database: python data/process_data.py data/disaster_messages.csv data/disaster_categories.csv data/DisasterResponse.db
- run the 'train_classifier.py' to train an save the model (note: only half of the data is loaded, to save computational power, edited line 31 and 32 to modify it): python models/train_classifier.py data/DisasterResponse.db models/classifier.pkl
- cd into the app directory and run 'python run.py'
- install required packages by run 'pip install -r requirements.txt'
- open http://0.0.0.0:3001/ on your browser to view the web app

## About the Data <a name="about-the-data"/>
There are two datasets used to train and test the model:
- disaster_categories.csv: contains multilabel categories for each message
- disaster_messages.csv: contains the actual text messages, both in the original language as well as in English

The data is highly imbalanced. One category does not even have a single count.

## About the Methods <a name="about-the-methods"/>
The python script 'process_data.py' is used to clean the data.
Categories are split into single columns. Column names for each category are given. Duplicates are removed as well as one category which has no counts. 
Both datasets are concatenated to one dataset. And finally it is saved to a sql database.

The python script 'train_classifier.py' generates the machine learning model.
The english text messages are tokenized, lemmatized and stop words are being removed. The model is build by using the CountVectorizer combined with the custom 
tokenizer and a tfidf transformer. MLSMOTE (Multilabel Synthetic Minority Over-sampling TEchnique) is used to oversample the train data. Random Forest Classifier combined with the MultiOutputClassifier from scikit is used for classification. The model is evaluated using the f1-score.

The oversampling is only applied to the train data. Therefore the vectorizer and the model is saved as a pickle file. Both are used to apply the model to new text 
messages in the web application. For future work a pipeline including vectorizer and MLSMOTE can be used as imblearn pipeline does not support multilabel yet.

Due to lack of computational power only about half of the data is used to train the model. One can change this in 'train_classifier.py' line 31 and 32 by loading all rows.

## Web Application <a name="webpage"/>
Screenshots from the webpage:
1. Navbar with link to Udacity and Github Repo. In the top there is the input for a text message to process it in the model.
![Top section of the webpage](https://github.com/LollaPie/Data_Science_Disaster_Response/blob/main/images/Screenshot_1.png?raw=true)

2. Two plots of the distributions of categories and genres in the dataset.
![Bar chart of the categories](https://github.com/LollaPie/Data_Science_Disaster_Response/blob/main/images/Screenshot_2.png?raw=true)
![Pie chart of the genres](https://github.com/LollaPie/Data_Science_Disaster_Response/blob/main/images/Screenshot_3.png?raw=true)

## Acknowledgements & Licensing <a name="acknowledgements--licensing"/>
Credits to Figure Eight Inc. to provide the data and Udacity to provide the course and the support.
