# BSM_Analytics
### Final capstone project for General Assembly's Data Science Immersive.

#### Executive Summary:
##### Intro and Goals:
The idea is to automate the process of providing moving estimates for a small DC-based moving company. Clients submit a short form with data about their origin and destination addresses, the number of boxes and furniture they have, and categorical variables about the type of places they're moving out of or into. Currently, a team of admin staff respond with estimates of how long the move will likely take, and whether it requires a big truck or a small truck.

The goals, therefore, are to provide accurate estimates of how many hours a client ends up being billed for AND replicate the human estimate process by predicting how many hours a human is likely to estimate the job will take. A hierarchical model is required, where binary classification (big truck or small) occurs first, then two separate models are trained on the data for big and small truck jobs, respectively. Additionally, a model can predict whether a job will take more or less time than estimated by a human.

##### Model Performance:

Since many big trucks jobs can and do handle jobs small enough for a small truck, the model must be highly sensitive to classifying small truck jobs. The classification model achieves 90% true positive rate in classifying small truck jobs, based on a validation set. 

The small truck model achieves an R-squared in the same ballpark as the admin team, or 'human estimator.' There is a lot of room for improvement here, in particular by encoding ordinal variables better, and hard coding more NLP tests against the client's list of furniture. 


##### Insights:

The model that predicts whether a job will take longer or less than the estimate achieves an AUC-ROC curve score of .7. There is room for improvement here as well, but I consider this a preliminary success since the model is trying to capture exactly what a team of human estimators cannot predict. The most important features in this model turned out to be: driving distance (computing using the Google Maps API), square footage at each location, the length of the list of furniture (in characters), sentiment analysis (polarity and subjectivity) on the furniture listing, and only then the number of boxes and the number of noun phrases in the furniture listing. Sentiment analysis on the 'extra comments' text field also turned out to be predictive of whether a job would take less or more time than the estimate. These results point to which variables human estimators should try and pay closer attention to.


##### Future Work:

Currently, the model counts the raw length of and number of noun phrases in client-submitted furniture listings, plus performs lemmatization and turns the top 100 most common words into vectors for prediction. Unfortunately, this has the effect of turning a word like 'bookshelves' into 'bookshelf' and ignores the difference between '5 couches' and 'a couch.' Future work will include hard coding a series of functions to count the occurence of common furniture types. I will also consult with stakeholders and the current human estimators to identify proven variables to track or patterns to search for.


#### README:

The data is read in from an Excel file in 00-Initial_EDA.ipynb, and initial data cleaning is done. A pickled dataframe is saved.

In notebooks 01-04, features are engineered.

A train test split is performed in notebook 05, and a count vectorizer is trained on the training set and applied to the test set. Final data cleaning and null value imputation is performed here, so imputation can be revisited in future work.

Notebooks 06-09 can be run independently. Each calls the pickled training data and outputs a pickled model. Models are *not* saved to GitHub, but can be reproduced by running the corresponding notebook.

Notebook 10 loads in the test data and models, but thus far the test data has not beeen evaluated against. I consider this project just a technical prototype, and I plan to engineer further features and finish the 'big truck' model before I do final evaluation.

#### 
Slides for a presentation I gave on this project are [here](https://docs.google.com/presentation/d/1-wq20dNEjY2UOmeaxaTDCcwVVN0oHdxpywIXMouA6J4/edit?usp=sharing)
