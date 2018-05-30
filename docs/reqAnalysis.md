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


### Testing 

For both approaches, we will use the standard metrics of testing for shallow and deep learning. This will include shuffling of training splits, cross validation, and in depth classification reports measuring the accuracy, precision, and recall to understand exactly what is happenign with the algorithms. 

The optimal scenario would be to have enough data for the network to train completely on one set and only touch the test set once for everytime it is testing. However, given how much viable data that is available, this may not be what actually happens. 

For the networks, it is very important that we do not fall prey to overfitting the test data. Hopefully, with a lot of data from the distributor we can avoid this problem. 