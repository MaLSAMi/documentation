#### Shallow Learning

Shallow Learning represents the techniques that are not 'deep learning' or in the case of this project, those of which do not utilize a neural network or multi-layer perceptron. The algorithms that will be tested under the topic of 'shallow learning' are Support Vector Machines, k-Nearest Neibhbors (kNN), Logistic Regression, Gaussian Naive Bayes, and Decision Trees/Random Forests. These algorithms' performances should give insight into the types of data we are seeing. From this, we can decide on better ways to fit the data. 


### Logistic Regression/Classification

We simply took the original feed forward network and removed the hidden layer to fit it with the data. Like the neural networks, we initialized with random weights and then trained it extensively to find the correct weights. This falls under the same stochastic error problems as a neural network does. 

The logistic regression approach is similiar to the Feed Forward Neural Network without the hidden layer. As the name suggests, we can use logistic regression simplly for predicting a continuous value. 

## One vs. Rest

A common classification problem. This is classifying a certain subset of the data as 'relevant' and the rest of the data as 'irrelevant'. 


## One vs One (Characterizing certain as relevant and the others as irrelevant)

Similiar to one vs one, however we are characterizing the irrelevant subset of data as being of one class while the 'relevant' subset is of another class. 


### Naive Bayes Algorithm

Implement naive bayes algorithm


### Support Vector Machines

We fitted a support vector machine with a polynomial kernel. For completeness, we added functionality for grid search (GridSearchCV) which fits the support vector machine with multiple different hyperparameters. (Note about the grid search, it is an exhaustive execution that will take a lot of time and energy. We recommend enabling GPU support, however it is unclear whether or not performance will ampify as much as it would for deep learning. Do not be surprised by long computation time. A quicker alternative would be to manually tune the hyperparameters with a training and validation set). 

In general, the Support Vector Machines with the Gaussian kernels perform optimally. 

### K-Nearest Neighbors

Very simple approach that is good for determining locality of data. Could be useful for clustering and dimension reduction. This method does not scale well with extra features/dimensions and so is not a viable choice. However, it is a fairly easy algorithm as it barely takes any training time. However, depending on the value of 'K', the classification for new tasks could take some time. 

### Random Forests/Decision Trees 

Random Forests are cool. Its main benefit is the ease of use and the quick classification. Furthemore, it does not require as much of a preprocessing as other algorithms as it can deal with virtually any kind of data. This is a viable candidate for the online learning as it will be useful in performing quick classification with likely high accuracy. 

The random forest is good to prevent overfitting from a decision tree. 


It is unlikely that the decision tree would perform better that the random forest. For completeness, we will first the data with the decision tree and use the results to better build the random forest to better fit the model. 

These random forests have numerous different applications and could very well fit this data will. 

















### Suppor Vector Machines

Suppor Vector machines are effective classifiers for any kind of classification task. A linear support vector machine is unlikely to linearly separate the data and so a polynomial is the first hypothesized choice. However, for completeness, we will train several different models on the data to obtain the best fit. Although this is an exhaustive process, support vector machines are relatively lightweight and very high regarded for classification tasks. Additionally, the preproccesing step to divide the classes into respective classification assignments is also important and will assist in more accuracte predictions. 

### K-Nearest Neighbor 

This is a simple clustering technique. An unlikely optimal fitting algorithm, but must be tested for completeness and comparison. The benefit of this approach is its ability to handle noisy and large amounts of data in a relatively simple way. Noisy and faulty data is very likely to happen in this case with all the data that will be gathered by the distributor. However, data with multiple features will not be well represented by this algorithm as it fails to scale in multiple dimensions. The accuracy (or non-accuracy) of this algorithm will give insight into the number of features and the natural grouping of the data. This can asssist in the other more specialized neural networks (most notably the convolutional neural networks). 


### Logistic Regression

This approach is good at formulizing a pattern based on the previous data analyzed. The issues are its likeliness to overfit while trying to learn more complicated data. However, when there is not much noise in the data, this algorithm is likely to perform very well as it can easily establish a relationship which explains not only the learned data but also to predict newer data. This algorithm will be useful in understanding any kind of correlation or imminent structure in the data. Logistic Regression is easy to optimize because of its convex objective function. 

### Gaussian Naive Bayes 

A simple and easy algorithm that should be the baseline performance in which the other algorithms are measured. A simple math formula which is easy to calculate and requires virtually no extra overhead. 

### Decision Trees/Random Forest

Decision Trees are beneficial for their ability to process and classify virtually any type of data. Random Forests are more advanced version of decision trees and usually perform very well. Both can be tested. However, the random forest is the more likely algorithm. 

target: online scheduling on RT systems


