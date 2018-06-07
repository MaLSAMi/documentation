# Requirements Analysis for MaLSAMi (Machine Learning based Schedulability Analysis for inter device Migration of software based components during Runtime)

## Overview

 Tasks are running on multiple electronic computing units (ECU). These ECUs periodically create checkpoints of the current state and progress of the running tasks. At some point in time, an ECU might fail. From the checkpoints and the information of the running tasks, the ECU must make a decision for migration of tasks on a failed ECU. This project hopes to utilize schedulability analysis to make better decisions on the migration of these components. After the ECU makes its decision, it must restore the checkpoint on another ECU and have that ECU execute the remaining tasks. 
	

The migration of a task by restoring a checkpoint to another ECU could happen either directly to another ECU or by collecting all the checkpoints of all the ECUs to a different machine and redistributing them to a chosen target ECU when necessary. Another variant of checkpointing would be to create an initial full checkpoint followed by smaller change-based incremental checkpoints. These incremental checkpoints might be integrated into the full checkpoint on the same ECU before sending it to another machine, or every checkpoint is sent right after creation. These smaller based checkpoints are motivated by the necessity of storing and retaining information in the event of an imminent failure. Furthermore, the data would prove to be useful for later analysis. 

Another possible use-case for checkpoints, which is not being looked into is the restart of failed tasks at its last known state on the same machine.

The decision of where a task is migrated to is generally based on the information about the task. It could also be a posibillity to include the information gained through the checkpoints to find the best solution.

We have chosen to employ [machine learning](machine_learning.md) to improve our ability to make these decisions. There are three general phases in which learning would be best applied: 


* **Offline Learning** Heavyweight phase where there is a lot of data available and enough resources to extensively train the model. We can train on previously sampled data and can utilize our resources for complicated algorithms. This will be done on a different ECU or computer to analyze as much data  as possible and to perform migration planning.
* **Online Learning** This type of online learning will be performed on very strong ECUs. Although these ECUs are strong, we do not have access to the entire dataset and all the resources as we are in the offline learning. Furthermore, we will be learning on data in real-time and will not be able to analyze both ends of the dataset. However, this aspect is necessary as it will simulate the migration planning in real time. These decisions will most likely have a greateer influence on the migration planning. 
* **online on normal ECUs (embedded boards)** This is similiar to the online learning phase described before. The only difference is that the ECU will not be as powerful and may require even lighter weight algorithms. 


## What we have

### Hardware Available

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

* Python 3.5.2
* Pytorch va
* Cuda v
* Qemu 
* Genode
* cxxnet
* Theano
* Torch7

## What we can do

Multiple frameworks for deep learning and parallel programming. 

Pytorch allows easy high level implementation of deep neural networks along with GPU accelerated computation. This will be especially useful in accelerating computation of deep neural networks. These GPUs will allow the networks to train on more data in less time. This feature will be especially useful when during the offline training phase where we can train deep and expansive nueral networks with full use of resources.   

There are numerous other frameworks that can also be utilized. Pytorch is good because of its ease in utilizing GPU architecture with neural networks. However, there are numerous other libraries that are specialized to the type of network or learning technique we are using. Cuda-convnet is another project that utilizes C++ Cuda implementatoin of neural networks. If we observe that the neural networks are performing well and we want to optimize, we can then pursue these libraries. 

Shallow Learning techniques are much simpler than Deep Learning techniques and do not always require very sophisticated libraries or hardware. Furthermore, whether or not the learning phase can or should be parallelized can be decided later. Given the resources, we have for the offline training phase, we will attempt to parallelize and optimize the algorithms wherever possible. 

After these rudimentary shallow and deep learning techniques are applied. We can look into reinforcement learning, a newer machine learning approach that is especially used for autonomous driving. The main difference between reinforcement learning and regular supervised/unsupervised machine learning is how an agent decides which actions to take based on the environment. We are currently mostly concerned with schedulablitity analysis, which will be learned based on the data itself. However, further analysis of the acquired data and the patterns analyzed may bring some interest into this type of approach. Other preprocessing and/or unsupervised learning techniques can be implemented to enhance the analysis. This will all depend on the data and the patterns that emerge when it is sampled. The ECUs allow us to use multiple forms of information which will be helpful for machine learning training such as lidar, radars, etc. 

### Checkpointing

Current state and snapshot of resources could be used for restarting in case of ECU failure or other problems. Learning can be done by continually monitoring these states and then using them as inputs into the machine learning models. 

Deep Learning would react better to this as it would be able to properly account for different kinds of input better than shallow learning techniques. Furthermore, the more sophisticated/complicated the data, the more likely that deep learning will perform better.  

Reinforcement Learning would be helpful in the checkpointing as it will be able to decide whether or not it wants to add a checkpoint based on its environment and available states. Obviously, if the probability of an ecu failing in a particular environment is high, it would be a good idea to add a checkpoint. These are areas that reinforcement learning would be better able to handle rather than regular shallow/deep learning. 

### Learning
When it comes to learning techniques, there are many options. MaLSAMi is going to look into Deep and Shallow Learning based data analysis and decision making.

#### [Deep Learning](Deep_Learning.md)

Deep Learning works best when there is a lot of data to sample from. These algorithms will be mostly utilized in the 'offline' phase of the learning. Deep Learning has a variety of different neural network models such as Generative Adversarial Networks (GAN), Spiking Neural Networks (SNN), Feed Forward Networks (FNN), Recurrent Neural Networks (RNN) and Convolutional  CNN.  These networks are specializied for specific types of data mining and analysis and are never a 'one fits all' model. Therefore, we plan to analyze several of these different models. Each of the networks listed below are catered to a certain kind of problem, but they are not too specialized to be unadaptable. 

### [Shallow Learning](Shallow_Learning.md)

Shallow Learning techniques are usually much simpler than deep learning. These require less time and energy to train and classify. However, as they are simpler, they do not have the same adaptibility of the neural networks. However, certain algorithms (Support Vector Machines and Random Forest) have proven to be quite effective in binary classifiaction. The aim of the shallow learning is to do an expansive test of different algorithms and understand what their fitting on the data indicates. High accuracy on certain algorithms will indicate different trends in the data. Regardless of whether or not shallow learning is used, these algorithms will bring more insight into the modelling of the data. 


### Testing 

For both approaches, we will use the standard metrics of testing for shallow and deep learning. This will include shuffling of training splits, cross validation, and in depth classification reports measuring the accuracy, precision, and recall. The challenges with data mining is dealing with improper and unclean data. Optimally, we would have enough data for extensive testing. Hopefully, the distributor will be able to generate enough worthwhile data to train on. 