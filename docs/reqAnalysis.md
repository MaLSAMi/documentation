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

Which data can be aquired from the distributor is dependent on the defined monitor, but the most information that can be gained are the parameters of each taskset, which were handed over to the genode operating system, and also the start and stop times of each job of each task and also the exit value.

### Available Software

Python 3.5.2
Pytorch va
Cuda v
Qemu 
Genode
cxxnet
Theano
Torch7

##What we can do

Multiple frameworks for deep learning and parallel programming. 

Pytorch allows easy high level implementation of deep neural networks along with GPU accelerated computation. This will be especially useful in speeding pu computation of deep neural networks. These GPUs will allow the networks to train on more data in less time. This feature will be especially useful when during the offline training phase, as this is where the GPUs are available.  

There are numerous other frameworks that can be used as well. It is difficult to say which is optimal and usually they all are highly capable. Pytorch is good because of its ease in utilizing GPU architecture with neural networks. However, there are numerous other libraries that are specialized to the type of network or learning technique we are using. Cuda-convnet is another project that utilizes C++ Cuda implementatoin of neural networks. If we observe that the neural networks are performing well and we want to optimize, we can then pursue these libraries. 

Shallow Learning techniques are much simpler than Deep Learning techniques and do not always require very sophisticated libraries. Furthermore, whether or not the learning phase can or should be parallelized can be decided later. 

Given the resources, we have for the offline training phase, we will attempt to parallelize and optimize the algorithms wherever possible. 

After these rudimentary shallow and deep learning techniques are applied. We can look into reinforcement learning, a newer machine learning approach that is especially used for autonomous driving. The main difference between reinforcement learning and regular supervised/unsupervised machine learning is how an agent decides which actions to take based on the environment. We are currently mostly concerned with schedulablitity analysis, which will be learned based on the data itself. However, further analysis of the acquired data and the patterns analyzed may bring some interest into this type of approach. 


The ECUs allow us to use multiple forms of information which will be helpful for machine learning training such as lidar, radars, etc. 

### Checkpointing

Current state and snapshot of resources could be used for restarting in case of ECU failure or other problems. Learning can be done by continually monitoring these states and then using them as inputs into the machine learning models. 

Deep Learning would react better to this as it would be able to properly account for different kinds of input better than shallow learning techniques. Furthermore, the more sophisticated/complicated the data, the more likely that deep learning will perform better.  

Reinforcement Learning would be helpful in the checkpointing as it will be able to decide whether or not it wants to add a checkpoint based on its environment and available states. Obviously, if the probability of an ecu failing in a particular environment is high, it would be a good idea to add a checkpoint. These are areas that reinforcement learning would be better able to handle rather than regular shallow/deep learning. 

### Learning
When it comes to learning techniques, there are many options. MaLSAMi is going to look into Deep and Shallow Learning based data analysis and decision making.

#### Deep Learning
Deep Learning works best when there is a lot of data to sample from. These algorithms will be mostly utilized in the 'offline' phase of the learning. Deep Learning has a variety of different neural network models such as Generative Adversarial Networks (GAN), Spiking Neural Networks (SNN), Feed Forward Networks (FNN), Recurrent Neural Networks (RNN) and Convolutional  CNN.  These networks are specializied for specific types of data mining and analysis and are never a 'one fits all' model. Therefore, we plan to analyze several of these different models. Each of the networks listed below are catered to a certain kind of problem, but they are not too specialized to be unadaptable. 


#### GAN
A GAN generally does not describe the structure of the neural network, but rather that there are two types of neural networks which work together (or against each other). One generates data similar to some real dataset and the second network, which was formerly trained on the original dataset evaluates the generated data. The generator intends on "fooling" the evaluating network into classifying the generated data as real. While training, the generator becomes better at creating data close to the real dataset and the evaluating network becomes better at flagging faulty or erroneous data. 

Typically the generator is a deconvolutional network, often generating images, while the second network is a convolutional network, evaluating the image.

#### RNN

A Recurrent Neural Networks are a type of network which utilizes 'memory'. These networks are very similiar to regular feed forward networks except for their ability to process previously analyzed along with current data. These types of networks are especially beneficial for temporal behavior. This type of network could prove to be fruitful in the online learning phase as this network can better analyze recent events and use them in the learning process. At the same time, thie network will still be heavy duty and possibly computationally more expensive than the regular feed-forward network. 


#### SNN

Spiking Neural Networks refer to any network in which the input nodes(neurons) propogate the information at different times throughout the network. Each input neuron has an activation level in which incoming spikes determines pushes the function higher or lower. These networks most closely model real networks in the brain, as all potential information is not fully processed at each time. The problem is that spiking is a noisy process, and may give a lot of unecessary information. The spikes are part of the learning process, and so the times the neurons are activated is analyzed just as much as what the neurons are sending. The idea of spiking can be applied to any of the other neural networks above, as it resembles more of a hyperparameter than an actual unique network model. A network using spiking is difficult to train as the signal nature of the spikes may be non-continuous and non-differentiable. 

#### CNN

A convolutional networks biggest strength is in its ability to extract the relevant features from an extremely large dataset. Convolutional networks are usually used in image processing as they are effective at processing images based on the information different areas of the image gives. Other than image processing, these types of networks are very good at measuring structured information. This includes text classificatoin and other problems in which the data's placement gives clues as to its meaning. If the data from the distributor happens to be structured in any way, the convolutional network has a good chance of performing well on it. 


#### FNN
In a previous Bachelors Thesis a student achieved some learning on a very simple FFN classifyer. A feed forward network should be one of the first networks to train as it is the simplest of the network models which propogates each data point forward and fits the model accordingly. If a high accuracy is attainable through this network, then it will indicate that the data is not too complicated and can be fit with pretty standard algorithms. Furthermore, analyzing and constructing a FFN network and its learning process is much simpler than any of the networks listed above. 





#### Shallow Learning

Shallow Learning represents the techniques that are not 'deep learning' or in the case of this project, those of which do not utilize a neural network or multi-layer perceptron. The algorithms that will be tested under the topic of 'shallow learning' are Support Vector Machines, k-Nearest Neibhbors (kNN), Logistic Regression, Gaussian Naive Bayes, and Decision Trees/Random Forests. These algorithms' performances should give insight into the types of data we are seeing. From this, we can decide on better ways to fit the data. 

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
