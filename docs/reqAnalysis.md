# Requirements Analysis for MaLSAMi (Machine Learning based Schedulability Analysis for inter device Migration of software based components during Runtime)

## What we want to do
on multi ecu system: 
	- tasks are running on multiple electronic computing units (ECU).
	- on each ECU checkpoints of the current progress of the running tasks are created
	- at some point in time a ECU might fail, then, based on information about the running tasks, a decision for migration of the tasks on the failed ECU has to be made.
	- for this decision some kind of schedulability analysis is necessary.
	- after a decision is made, the checkpoint has to be restored on another ECU and all tasks should continue to run


Creating checkpoints of running tasks could include the memory, the assigned capabilities or the registers.
After an initial full checkpoint an incremental approach to saving changes is also a posibility.

The migration of a task by restoring a checkpoint to another ECU could happen either directly to another ECU or by collecting all the checkpoints of all the ECUs to a different machine and redistributing them to a choesen target ECU when necessary.

"""""""""""""""""incremental checkpoints / restore tasks on same machine with last one / sending incrementals after initial full one, distribute stuff

sched analysis ->
learning in 3 phasen (shallow /deep)
	offline
	online mit performanter hardware
	online mit embedded boards

what learning is helping?
	GAN (digitaler zwilling?)
	Spiking Neural Networks (SNN)
	FNN
	RNN
	CNN

TODO research: evaluation time/training time directly dependant on  width /depth of network
target: online scheduling on RT systems
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

Which data can be acuired from the distributor is dependant on the defined monitor, but the most information that can be gained are the parameters of each taskset, and the start and stop times of each job of each task

### Used Software

Python 3.5.2
Pytorch v
Cuda v
Qemu 
Genode
