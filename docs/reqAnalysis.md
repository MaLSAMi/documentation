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
TODO
####CNN
TODO
####FNN
In a previous Bachelors Thesis a student achieved some learning on a very simple FFN classifyer. 





TODO: add varuns learning part


target: online scheduling on RT systems
