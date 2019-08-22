# Datageneration 

The implementation responsible for forming the tasks and as a result the tasksets for deployment is in the datageneration repository in the MaLSAMI project. The tasksets are incrementally created beginning with taksets of size one (each taskset consists of one task each) and then are continually created to build tasksets as big as size four (4 tasks per taskset). The progression works as follows:
1. At first a certain amount of tasks(different parameter configurations) for each available task type are created.
2. These tasks are then executed as tasksets of size one and categorized into successful (good) and unsuccessful (bad) tasksets.

The next steps are repeated after the tasksets of the current size are all executed:
3. To create tasksets of size n, take all 'good' tasksets of size n-1 and combine them with each 'good' taskset of size 1.
4. Then execute and categorize.

Combining only tasksets that are known to be successful is meant to limit the combinatorial explosion. But even with this approach, numbers grow rapidly.


## Parameters of our Data

```python
	'PRIORITY': (1,5),
	'DEADLINE' : (0, 0),
	'PERIOD': (1,8),
	'CRITICALTIME' : (0, 0),
	'NUMBEROFJOBS': (1,8),
	'OFFSET': (0,0),
	'QUOTA': (100, 100),
	'CAPS': (235, 235),
	'CORES' : (0, 0),
	'COREOFFSET' : (0, 0),
	'ARG':
			{'hey':(0,0),
			'pi':(13,21),
			'tumatmul':(12,19),
			'cond_mod':(25,30)
			}
```

Because we limit the PERIOD to whole seconds it is possible that tasks are blocking each other, which might not have happened if the value was less discrete.

## Below is a brief description of the important files: 



### data_parser.py

The entire taskset data is stored in the log files for bookkeeping. For analysis, this file parses the log files in the chosen directory and stores into a databse. SQLite was used in this implementation but functionality for other mySQL databases should be possible as well. SQL is recommended because of the ease of querying and the connection between the databases. 

The database consists of these three Tables: 


1] Job

2] Task

3] TaskSet


1] Job table consists of all the jobs and its respective attributes. It also contains a column for the TaskID which referes to the Task that it was placed in and a SetID column which refers to the TaskSetID that it is a part of. 

2] The *Task* table consists of all the tasks that were deployed by the distributor. The attributes include the "Priority", "Deadline", and "Number of Jobs". It's primary key is its TaskID which is decided upon by the taskset. 

3] The *TaskSet* table consists of all the Tasksets and is primarily referenced through its SetID. It also contains the IDs of all the Tasks and has a column indicating if the respective TaskSet was successful or not. Each Taskset has *n* columns which corresponds to n Tasks in the respective TaskSet. For a TaskSet of size k < n. The first *k* columns each contain the respective TaskIDs and the remaining contain *-1*, indicating that the columns are empty. 


Here are some example queries to query the database for a dataset: 

Get TaskSets of size *1*: 

```sqlite3
select TaskSet.Set_ID, Task.*, TaskSet.Successful 
 from Task 
 inner join TaskSet on Task.Task_ID = TaskSet.TASK1_ID 
``` 

 Get TaskSets of size *3*: 

 ```sqlite3
 select TaskSet.Set_ID, t1.*, t2.*, t3.*, TaskSet.Successful '
  from Task t1, Task t2, Task t3 
  inner join TaskSet on t1.Task_ID = TaskSet.TASK1_ID 
  and 
  t2.Task_ID = TaskSet.TASK2_ID 
  and 
  t3.Task_ID = TaskSet.TASK3_ID 
  and TaskSet.TASK4_ID = -1 
```


  **NOTE**: These quereies were performed for a SQLite database. Other databases may have differences.

### make\_tasks.py

This calls a helper function in the *parameter\_config.py* to generate a file per task type defined in the *parameter\_config.taskTypes*. Each file consists of *parameter\_config.linesPerCall* lines and each line is a list of hash values with *parameter\_config.tasksPerLine* values.

### main.py

The *main.py* can be called without argument, but for each task in *parameter\_config.taskTypes* there has to exist a file (created by executing *make\_tasks.py*). *main.py* can also be called with the argument **c** to continue the execution with data loaded from the following files: *bad\_tasksets*, *good\_tasksets* and, if available, *possible\_tasksets*. These contain information gained by a previous execution of *main.py*.

Other options: 

**ss** - 'Show Status'. Print current status of the data generation and the current length of all the task lists

**h** - Halt Machines

**k** - Kill all Machines 

**s** - Save current progress

**x** - Clean exit 



## Helper Functions

### parameter\_config.py

This file contains all the parameters of the variables and data structure we use for the data generation. 

Parameter are randomly chosen within a range of suitable values. ("Priority": (1,5) indicates that a random task will be generated with a random value between 1 and 5. ) This file is referenced numerous time in the data creation while specifying parameters. 

For easy book-keeping and facilitated reading and writing to file, the parameters are stored in a concatenated strings before the main task generation is made. This ensure uniqueness and also an easy reference to the tasks and the tasksets. 



### value\_init.py

This file will initiate the values of the tasks according to the parameter values in parameter_config. This creates the Task object as a list of dictionaries. This package is called from make\_takss.py and with the appropriate parameters which include the number of tasks to make and the package. Depending on the package chosen, the appropriate package will be populated with the selected number of tasks chosen. 

Additionally, this file provides functions for plotting the distribution of the parameters of the tasksets. 

