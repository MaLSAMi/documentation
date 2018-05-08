### Shallow Learning

Add documentation about Shallow Learning approaches



### Logistic Regression/Classification

We simply took the original feed forward network and removed the hidden layer to fit it with the data. Like the neural networks, we initialized with random weights and then trained it extensively to find the correct weights. This falls under the same stochastic error problems as a neural network does. 

The logistic regression approach is similiar to the Feed Forward Neural Network without the hidden layer. As the name suggests, we can use logistic regression simplly for predicting a continuous value. 

## One vs. Rest

## One vs One (Characterizing certain as relevant and the others as irrelevant)


### Naive Bayes Algorithm

Implement naive bayes algorithm


### Support Vector Machines

We fitted a support vector machine with a polynomial kernel. For completeness, we added functionality for grid search (GridSearchCV) which fits the support vector machine with multiple different hyperparameters. (Note about the grid search, it is an exhaustive execution that will take a lot of time and energy. We recommend enabling GPU support, however it is unclear whether or not performance will ampify as much as it would for deep learning. Do not be surprised by long computation time. A quicker alternative would be to manually tune the hyperparameters with a training and validation set). 

### K-Nearest Neighbors

Very simple approach that is good for determining locality of data. Could be useful for clustering and dimension reduction. This method does not scale well with extra features/dimensions and so is not a viable choice. However, it is a fairly easy algorithm as it barely takes any training time. However, depending on the value of 'K', the classification for new tasks could take some time. 

### Random Forests/Decision Trees 

Random Forests are cool. Its main benefit is the ease of use and the quick classification. Furthemore, it does not require as much of a preprocessing as other algorithms as it can deal with virtually any kind of data. This is a viable candidate for the online learning as it will be useful in performing quick classification with likely high accuracy. 

The random forest is good to prevent overfitting from a decision tree. 


It is unlikely that the decision tree would perform better that the random forest. For completeness, we will first the data with the decision tree and use the results to better build the random forest to better fit the model. 

These random forests have numerous different applications and could very well fit this data will. 

