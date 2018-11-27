Given the nature of the original data, the parameters were not too different and it was difficult to do any machine learning tasks on it. Furthermore, the parameters used were not too descriptive. For the new data, we are making use of newer parameters **priority, deadline, period, critical time, number of jobs, offset, quota, caps, cores, core offset, arg**.

taskParameters = {	'PKG':
						{1:'hey',
						 2:'pi',
						 3:'tumatmul',
						 4:'cond_mod'#,
						 #5:'cond_42'
						},
				'PRIORITY': (1,5),#127), # think we can put constraint on this and just provide maybe 5 different values, so values appear more often and in the end with fp scheduling only the difference should matter(?)
				'DEADLINE' : (0, 0),
				'PERIOD': (1,8),
				'CRITICALTIME' : (0, 0), # is assigned by function depending on PERIOD
				'NUMBEROFJOBS': (1,8),#(1,10),
				'OFFSET': (0,0),
				'QUOTA': (100, 100), #(1, 100),# we could just assign arbitrary big values to this and to caps as well, cause a working task, which is the assumption for an initial taskset, would have good values for that and both (caps and ram) are available in abundance 
				'CAPS': (235, 235), #(10, 235)
				'CORES' : (0, 0),
				'COREOFFSET' : (0, 0),
				'ARG':
						{'hey':(0,0),#23-28
						'pi':(13,21),#84-1600
						'tumatmul':(12,19),#104-2700
						'cond_mod':(25,30)#,#130-3000
						#'cond_42':(2,4)
						}
				}


In the example above, the indicated values (a,b) indicates the parameter value will be in the range between a and b. As shown above, some parameters such as *CAPS*, *COREOFFSET*, *OFFSET*, *DEADLINE*, *QUOTA* will all remain constant due to how Genode works. Although we need these parameters in order to simulate the tasks, their constant nature will not give any further analysis in terms of Genode. Therefore, we will turn our focus to the parameters that are variable. This will give a better understanding on whether these parameters have any influence on success of the tasksets. 


