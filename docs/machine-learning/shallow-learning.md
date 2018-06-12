# Shallow Learning

Shallow Learning represents the techniques that are not 'deep learning' or in the case of this project, those of which do not utilize a neural network or multi-layer perceptron. Although virtually any technique can be tested under the guise of 'shallow learning', we chose to focus on Support Vector Machines, k-Nearest Neibhbors (kNN), Logistic Regression, Gaussian Naive Bayes, and Decision Trees/Random Forests. While these algorithms each have their strenghts and weaknesses, their lightweight and easy implementation makes them easy to test and analyze. From the performance of these various algorithms, we can find import trends in the data. 


### Logistic Regression/Classification

Logistic Regression will determine attempt to model any relationship between the measured data and the label data. In the case of taskset data, logistic regression will attemp to model a relationship between the various tasksets. 

If you are familiar with neural networks, logistic regression is simply a neural network without the hidden layer. It will give weights to the data point(s) based on the features.  


### Naive Bayes Algorithm

Naive Bayes algorithm is 'naive' because it implicity assumes independence among all individual training examples. As we know with data systems, let alone taskset data, it is very unlikely that the data is independent. However, if we were to get a good performance with this classificaton algorithm, it would inidcate that the data is uncorrelated. 

Although more sophisticated algorithms exist, naive bayes is very good for efficient computation. Because of its assumption of independence, the order of the input or the arrangement of the data does not affect the overall training experience. This is especially important in online-learning when all the data is not immediately available to us. 


### Support Vector Machines

We fitted a support vector machine with a polynomial kernel. For completeness, we added functionality for grid search (GridSearchCV) which fits the support vector machine with multiple different hyperparameters. (Note about the grid search, it is an exhaustive execution that will take a lot of time and energy. We recommend enabling GPU support, however it is unclear whether or not performance will ampify as much as it would for deep learning. Do not be surprised by long computation time. A quicker alternative would be to manually tune the hyperparameters with a training and validation set). 

In general, the Support Vector Machines with the Gaussian kernels perform optimally. 

### K-Nearest Neighbors

The K-Nearest Neighbors is one of the simples algorithm that uses rudimentary techniques to classify data. It is a flexible approach and can be useful for determining locality information. This information could further be used for unsupervised learning techniques such as clustering and dimension reduction. Unfortunately, this method does not scale well with multi-feature data similiar to the data that we currently have. However, this algorithm is fairly simple to implement and test. It will serve as a meaningful control algorithm (one in which we compare our fancier algorithms to). 

### Random Forests/Decision Trees 

Decision Trees are great for handling categorical information without having to do much preprocessing. After the training phase, it is able to classify data quickly. This will be especially useful in the online learning phase. The main issue with decision trees is its likelihood of overfitting. This is where random forests come in to the picture.  

Random Forests are a very powerful algorithm and handle the low variance issues of decision trees. Although they are a little more difficult to implement/tune, they are expected to be one of the more useful algorithms. Much like decision trees, they can classify test data very quickly.   


### Suppor Vector Machines (svm)


Suppor Vector machines are effective classifiers for any kind of classification task. A linear support vector machine  may not separate the data as well as a non-linear svm. However, for completeness, we will train several different models on the data to obtain the best fit. Although this is an exhaustive process, support vector machines are relatively lightweight and very highly regarded for binary classification tasks. Additionally, the preproccesing step to divide the classes into respective classification assignments is also important and will assist in more accuracte predictions. 




