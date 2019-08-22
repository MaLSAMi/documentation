Given the nature of the original data, the parameters were not too different and it was difficult to do any machine learning tasks on it. Furthermore, the parameters used were not too descriptive. For the new data, we are making use of newer parameters **priority, deadline, period, critical time, number of jobs, offset, quota, caps, cores, core offset, arg**.

<pre>
<code>

taskParameters = {	
    'PKG': 
					{1:'hey',
						 2:'pi',
						 3:'tumatmul',
						 4:'cond_mod'#,
						 #5:'cond_42'
						},
				'PRIORITY': (1,5) 
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
						{'hey':(0,0),#23-28
						'pi':(13,21),#84-1600
						'tumatmul':(12,19),#104-2700
						'cond_mod':(25,30)#,#130-3000
						}
				}

</code>
</pre>
In the example above, the indicated values (a,b) indicates the parameter value will be in the range between a and b. As shown above, some parameters such as *CAPS*, *COREOFFSET*, *OFFSET*, *DEADLINE*, *QUOTA* will all remain constant due to how Genode works. Although we need these parameters in order to simulate the tasks, their constant nature will not give any further analysis in terms of Genode. Therefore, we will turn our focus to the parameters that are variable. This will give a better understanding on whether these parameters have any influence on success of the tasksets. 



https://towardsdatascience.com/the-next-level-of-data-visualization-in-python-dd6e99039d5e