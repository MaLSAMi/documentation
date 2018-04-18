# Requirements Analysis for MaLSAMi (Machine Learning based Schedulability Analysis for inter device Migration of software based components during Runtime)

## What we want to do
on multi ecu system: 
	- tasks are running on multiple electronic computing units (ECU).
	- on each ECU checkpoints of the current state_/progress of the running tasks are created periodically
	- at some point in time a ECU might fail, then, based on information about the running tasks, a decision for migration of the tasks on the failed ECU has to be made.
	- for this decision some kind of schedulability analysis is necessary.
	- after a decision is made, the checkpoint has to be restored on another ECU and all tasks should continue to run


Creating checkpoints of running tasks could include the memory, the assigned capabilities or the registers.
After an initial full checkpoint an incremental approach to saving changes is also a posibility.

The migration of a task by restoring a checkpoint to another ECU could happen either directly to another ECU or by collecting all the checkpoints of all the ECUs to a different machine and redistributing them to a chosen target ECU when necessary.
Another variant of checkpointing would be to create an initial full checkpoint followed by smaller change-based incremental checkpoints. These incremental checkpoints might be integrated into the full checkpoint on the same ECU before sending it to another machine, or every checkpoint is sent right after creation.
A possible use-case for checkpoints, which is not being looked into is the restart of failed tasks at its last known state on the same machine.

The decision where a task is migrated to is mainly based on the general information about the task but it could also be a posibillity to include the information gained through the checkpoints to find the best solution.
Learning (of any kind) can be performed in three general categories: 
-offline on a different ECU or computer for exactly the purpose of analysing the data and performing the migration planning.
-online on very strong ECUs which are performing tasks and also the data analysis and decision making necessary for migration
-online on normal ECUs (embedded boards) which are performing tasks and also the data analysis and decision making necessary for migration


## What we have

### Hardware

3 Workstations:
-	titan V

-	3x gtx1080ti

-	2x tesla k20c
	quadro k4200

### Data

Checkpointing currently includes only the information in the memory. Checkpointing the capabilities or the registers is not possible yet.

No data yet, we will have to generate it using the implemented distributor.

Which data can be acuired from the distributor is dependant on the defined monitor, but the most information that can be gained are the parameters of each taskset, which were handed over to the genode operating system, and also the start and stop times of each job of each task and also the exit value.

### Available Software

Python 3.5.2
Pytorch v
Cuda v
Qemu 
Genode


##What we can do

### Checkpointing
TODO
-Use what David and Alex researched and turned out to work already.
-Research on checkpointing is not going to be part of MaLSAMi.


### Learning
When it comes to learning techniques, there are many options. MaLSAMi is going to look into Deep and Shallow Learning based data analysis and decision making.

####Deep Learning
When it comes to Deep Learning there exist a variety of neural network models like Generative Adversarial Networks (GAN), Spiking Neural Networks (SNN), Feed Forward Networks (FNN), Recurrent Neural Networks (RNN) or Convolutional  CNN, just to name a few. But neural networks are usually not a 'one fits all' type of model.

TODO research: evaluation time/training time directly dependant on  width /depth of network

####GAN
A GAN in general does not describe the structure of the used neural network, but that there are two types of neural networks which work together (or against each other). One generates data similar to some real dataset and the second network, which was formerly trained on the original dataset evaluates the generated data. The generator wants to "fool" the evaluating network into classifying the generated data as real. While training the generator becomes better at creating data close to the real dataset and the evaluating network is becoming better at flagging not real data.
Typically the generator is a deconvolutional network, often generating images, and the second network is a convolutional network, evaluating the image.

####RNN
A Recurrent Neural Networks are a type of network that utilizes 'memory'. These networks are very similiar to regular feed forward networks except for their ability to process previously analyzed data along with current data. These types of networks are especially beneficial for temporal or time behavior. This type of network could prove to be fruitful in the online learning phase as this network can better analyze recent events and use them in the learning process. At the same time, thie network will still be heavy duty and possibly computationally more expensive than the regular feed-forward network. 


####CNN

A convolutional networks biggest strenght is in its ability to extract important features when given a lot of information that it may not necessarily need. This would be useful if the distributor provides data with a lot of information that is not good for anything that always happens to find its way in the data. This is good for figuring out which information is useful in the learning process and which isn't. 

####FNN
In a previous Bachelors Thesis a student achieved some learning on a very simple FFN classifyer. A feed forward network should be one of the first networks to train as it is the simplest of the network models and its results will indicate whether more advanced networks are necessary. Similiarly, a simple and initial structure of the network will provide information about how the data is possible. Analysis of th learning of a FFN is much simpler than trying to analyze what is going on in the other structures above.  





####Shallow Learning

Shallow Learning represents the techniques that are not 'deep learning' or in the case of this project, those of which do not utilize a neural network or multi-layer perceptron. The algorithms that will be tested under the topic of 'shallow learning' are Support Vector Machines, k-Nearest Neibhbors (kNN), Logistic Regression, Gaussian Naive Bayes, and Decision Trees/Random Forests. Testing these algorithms will give insight into which kind of data we are seeing. From this information we can than better suit out models to provide the best type of learning possible.  

###Suppor Vector Machines

Suppor Vector machines are effective classifiers for any kind of mapping. A linear support vector machine is unlikely to linearly separate the data and so a polynomial estimate is the first hypothesized choice for testing. However, for completeness, we will use a grid search support vector machine fitting to find the optimal support vector machine. Grid searching is an exhaustive process and takes a lot of time. This is where increased cpu power will come in handy. Additionally, the preproccesing step to divide the classes into respective classification assignments is also important and will assist in more accuracte predictions. 

###K-Nearest Neighbor 

This is a simple clustering technique. An unlikely optimal fitting algorithm, but must be tested for completeness and control. The benefit of this approach is its ability to handle noisy and large amounts of data in a relatively simple way. Noisy and faulty data is very likely to happen in this case with all the data that will be gathered. However, data with multiple features will not be well represented by this algorithm. The prediction power of this algorithm drops drastically for every feature added. The accuracy (or non-accuracy) of this algorithm will give insight into the number of features and the natural grouping of the data. This can asssist in the other more specialized neural networks. 


###Logistic Regression

This approach is good at formulizing a pattern based on the previous data analyzed. The issues are its likeliness to overfit given a lot of data. However, when there is not much noise in the data, this algorithm is likely to perform very well as it can analyze patterns better than some of the more rudimentary algorithms. Furthermore, it is highly adept at understanding patterns and attempting to map all the data under a single formula. This can prove effective if the data appears to be correlated in any way. 

###Gaussian Naive Bayes 

A simple and easy algorithm that should be the baseline performance in which the other algorithms are measured. A simple math formula which is easy to calculate and requires virtually no extra overhead. 

###Decision Trees/Random Forest

Decision Trees are beneficial for their ability to process and classify virtually any type of data. Random Forests are more advanced version of decision trees and usually perform very well. Both can be tested. However, the random forest is the more likely algorithm. 

target: online scheduling on RT systems
