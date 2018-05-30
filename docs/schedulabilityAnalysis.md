Schedulability Analysis 

On real-time systems, tasks will be executed and processed on multiple different ECUs. These ECUs are responsible for various distributed tasks whose analysis is important for migration planning in the probable event of system failure. 

On multi-ecu systems, the ECUs hold information about the task such as the start/end time. In the event of an ECU failure, it must have a prevention/recovery method in which it can migrate unfinished tasks to other ECUs  that it has not been able to complete. The aim of the schedulability analysis is to 'learn' and 'analyze' from past events and previous scenarios for better damage control. 
	
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


The advantage of offline learning is that we are able to utilize virtually all of our resources and compute time to test multiple algorithms to fit the data. The disadvantage with this is that we will be dealing with a static datasets. Althought this does not imply that the dataset is erroneous, it is not akin to real time data that will happen at the online phase. 

Furthremore, heavy computation and time used to fit a static datasets very likely leads to overfitting. Even if appropriate measures are made, it is possible that the online data could be different from that of the dataset used. 

Analogously, the online training is beneficial and detrimental for the opposite reasons. While online, we do not have as much time and resources as we do while offline. Especially in the situation that we are in now, we must process the data quickly. Therefore, we used the online training as more of a 'validation' stage in which we fine tune the models and hyperparameters. 

The distributor is the module responsible for data generation that we will be used for the schedulability analysis. See the *[distributor file](distributor.md)* for more information about the distributor. 

To further analyze the methods we are using, view *[Machine Learning](machine_learning.md)* and the *[requirement analysis](reqAnalysis.md)*
