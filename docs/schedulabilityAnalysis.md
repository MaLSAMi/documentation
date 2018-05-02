Schedulability Analysis 

On real-time systems, taks will be ran and processed on multiple different ECUs. These ECUs are all responsible for various tasks that would be important for migration planning in the event of system failure. 

On multi ecu systems, the ECUs usually hold information about the task such as the start/end time. In the event of a very likely ECU failure, it must have a prevention/recovery method in which it can migrate unfinished tasks to other ECUs  that it has not been able to complete. The aim of the schedulability analysis is to 'learn' and 'analyze' from past events and previou scenarios for better damage control. 
	
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


The distributor is the module responsible for data generation that we will be used for the schedulability analysis. See the *distributor.md* file for more information about the distributor. 

To further analyze the methods we are using, view *machine_learning.md*. 
