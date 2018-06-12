# Monitor

This section is supposed to provide insight on the monitor component and how it is intended to be used. The monitor has to be provided alongside the taskset component to the _add\_jobs()_ function of the distributor. The monitors functions are called in _run()_ of the _machine.py_.

A monitor has to implement the _AbstractMonitor_ in the distributor\_service module which defines the following abstract methods:

#### _\_\_taskset\_event\_\_(taskset, event)_

  This function is called when the _session.run()_ as soon as new information about the taskset is returned from Genode.

#### _\_\_taskset\_start\_\_(taskset)_
   
  This function is called when a new taskset has benn started by calling the _session.start()_ function.

#### _\_\_taskset\_stop\_\_(taskset)_
   
  This function is called when a new taskset has benn started by calling the _session.stop()_ function. If this function is called the monitor regards the taskset as completed and all information, which could be gained is available. 

#### _\_\_taskset_finish\_\_(self, taskset)_

  

  In general the monitor functions always hold a reference to the taskset the function was called with, so it has access to all information saved in the obect defined by the [**task.py**](https://github.com/malsami/taskgen/blob/master/task.py).