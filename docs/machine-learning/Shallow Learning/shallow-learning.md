# Shallow Learning

Shallow Learning represents all the machine learning algorithms the techniques that are not 'deep learning' or in the case of this project, those of which do not utilize a layered-neural network or multi-layer perceptron. Although virtually any technique can be tested under the guise of 'shallow learning', we chose to focus on k-Nearest Neibhbors (kNN), Logistic Regression, Gaussian Naive Bayes, and Decision Trees/Random Forests (Support Vector Machine functionality is present, but the training was too long to extract meaningful results). The success of these algorithms is almost entirely dependent on the patterns that are present in the data. These algorithms have different strengths, and we are hoping to not only analyze how well these algorithms can perform, but also how they can be applied to embedded systems or online-machine learning. 

## Testing Setup

The shallow learning models were taken from the Sci-kit learn python class. The current machine learning pipeline allows the user to develop his or her own shallow learning models if he or she does not wish to use those of sci-kit learn. The Machine Learning Pipeline currently wraps the sci-kit learn machine learning models and some of the important methods. 

Popular evaluation metrics on data include data splitting (train, validation, testing sets), k-fold cross-validation, and parameterized grid search for optimal hyperparameter search. 

Given the extraordinary amount of time that grid search takes, a 'randomized' search was used instead. Both of these searches take a list of parameters specified by the user and cross checks them to obtain the best parameters. While a grid search will test every parameter value, the ranomized search searches only a small fraction of them. This is the default search that we used. The developer is welcome to revert to the exhaustive Grid search by toggling the parameter. However, the results presented below will show only the results done by a 'randomized' grid search and not an exhaustive one. 

Also, the parameters chosen were completely arbitrary. A developer may get different results not only from different hyperparameter selection, but also from different grid search runs. The grid search is only used to give a basic idea of what is going on. 

### Logistic Regression/Classification

Logistic Regression will determine attempt to model any relationship between the measured data and the label data. In the case of taskset data, logistic regression will attemp to model a relationship between the various tasksets. 

If you are familiar with neural networks, logistic regression is simply a neural network without the hidden layer. It will give weights to the data point(s) based on the features.  

**Randomized Grid Search Results on pandas data:**

*Best Penalty Type*: **L1**

*Best C (Regularization Strength)*: **1291.5496650148827**

(Rest are default parameters)

### Naive Bayes Algorithm

Naive Bayes algorithm is 'naive' because it implicity assumes independence among all individual training examples. As we know with data systems, let alone taskset data, it is very unlikely that the data is independent. However, if we were to get a good performance with this classificaton algorithm, it would inidcate that the data is uncorrelated. 

Although more sophisticated algorithms exist, naive bayes is very good for efficient computation. Because of its assumption of independence, the order of the input or the arrangement of the data does not affect the overall training experience. This is especially important in online-learning when all the data is not immediately available to us. 


### K-Nearest Neighbors

The K-Nearest Neighbors is one of the simples algorithm that uses rudimentary techniques to classify data. It is a flexible approach and can be useful for determining locality information. This information could further be used for unsupervised learning techniques such as clustering and dimension reduction. Unfortunately, this method does not scale well with multi-feature data similiar to the data that we currently have. However, this algorithm is fairly simple to implement and test. It will serve as a meaningful control algorithm (one in which we compare our fancier algorithms to). 

**Randomized Grid Search Results on pandas data:**

*Best Number of K-Neighbors*: **5**

(Rest are default parameters)


### Random Forests/Decision Trees 

Decision Trees are great for handling categorical information without having to do much preprocessing. After the training phase, it is able to classify data quickly. This will be especially useful in the online learning phase. The main issue with decision trees is its likelihood of overfitting. This is where random forests come in to the picture.  

Random Forests are a very powerful algorithm and handle the low variance issues of decision trees. Although they are a little more difficult to implement/tune, they are expected to be one of the more useful algorithms. Much like decision trees, they can classify test data very quickly.   

**Randomized Grid Search Results on pandas data:**

*Best Depth*: **70**

*Best Max Features*: **auto**

*Best min_samples_leaf*: **3**

*Best min_samples_split*: **4**

*Best n_estimators*: **1000**

(Rest are default sci-kit learn parameters)

### Suppor Vector Machines (svm)


Suppor Vector machines are effective classifiers for any kind of classification task. A linear support vector machine  may not separate the data as well as a non-linear svm. However, for completeness, we will train several different models on the data to obtain the best fit. Although this is an exhaustive process, support vector machines are relatively lightweight and very highly regarded for binary classification tasks. Additionally, the preproccesing step to divide the classes into respective classification assignments is also important and will assist in more accuracte predictions. 

We fitted a support vector machine with a polynomial kernel. For completeness, we added functionality for grid search (GridSearchCV) which fits the support vector machine with multiple different hyperparameters. (Note about the grid search, it is an exhaustive execution that will take a lot of time and energy. We recommend enabling GPU support, however it is unclear whether or not performance will ampify as much as it would for deep learning. Do not be surprised by long computation time. A quicker alternative would be to manually tune the hyperparameters with a training and validation set). 

In general, the Support Vector Machines with the Gaussian kernels perform optimally. 


