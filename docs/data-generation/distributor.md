# Distributor 

Distributor is the main class/entity that controls and distributes host sessions to manage tasksets. Upon startup, the distributor will have a preset value of one host session that it will be able to spawn. The user is permitted to change this number at any time up to a hardcoded limit of fortytwo (QEMU instances). Machines set to be closed will finish their assigned taskset before being shut down. The distributor is mainly used for gathering large-scale data about autonomous system schedulability-tasks, which can be used for data mining and analysis. 



## Set up and Configuration

Clone the client-tools repository, move to the client-tools directory and execute the make commands as shown below. The value "focnados_pbxa9" that is passed to the OS-TARGET argument can be substituted for the intended target.
```bash
git clone https://www.github.com/malsami/client-tools
cd client-tools
make distributor-init
make make genode-init
make binaries OS-TARGET=focnados_pbxa9
```

and initialize the submodules and place a working [image.elf](https://argos-research.github.io/documentation/) file inside the client-tools directory.

### With Vagrant

A **vagrant** script is provided in the client-tools repository, which will set up the appropriate development environment and prepare it for use without any manual installation or configuration.
This can be setup via
```bash
make vagrant
```
after telling vagrant to wich interface to connect, you will end up inside a vagrant machine.
If you 
```bash
cd /Vagrant
```
you will be in the mounted client-tools folder.

(In the past, executing the distributor inside a vagrant machine lead to an unknown error, which stops the execution at some point after about ten to thirty hours. As the vagrant machine serves only as a test and development environment, this is not a critical issue and will not be further investigated, as mentioned in the according [issue](https://github.com/malsami/distributor/issues/9). Whether this is still the case or not is unclear, as no distributor ran that long inside a vagrant machine ever again.)

### Manual Setup

To run the distrubutor directly on your system, the bridge functionality and networking components have to be installed.

Install bridge functionality for networking:


    sudo apt-get install bridge-utils -qq


Download DHCP service and move provided configuration file. 


    sudo apt-get install isc-dhcp-server -qq
    sudo cp dhcpd.conf /etc/dhcp/
    
Set up the bridge and assign an IP address (consult the dhcp.conf file for more information on IP ranges)


    sudo brctl addbr br0
    sudo ip addr add 10.200.45.254/24 dev br0


Adjust /etc/network/interfaces file with preliminary networking information


    sudo sh -c 'echo "\nauto br0\niface br0 inet static\n\thwaddress ether DE:AD:BE:EF:69:01\n\taddress 10.200.45.254\n\tnetmask 255.255.255.0\n\tgateway 10.200.45.254\nbridge_ports eth0\nbridge_stp off\nbridge_maxwait 0\nbridge_fd 0\n" >> /etc/network/interfaces'


Install qemu and screen for spawning host sessions from the distributor and for easy visualization of spawned sessions. 


    make qemu
    sudo apt-get install screen -qq

Start the dhcp service

    sudo systemctl start isc-dhcp-server


The machine should now be ready for use. 

## Using the Distributor

The following is an example execution to provide better understanding.
First change into the created python environment by typing

    source malsami/bin/activate

You are now inside the python environment. (To leave it just type "deactivate")

**Open up the interactive python shell** in the directory 'distributor' by typing (You can also create and execute this in a script)


    sudo python3

sudo is necessary to allow for the creation and destruction of tap devices, via which the qemu instances are connected to the bridge.


**Add appropriate imports:** 

('example.py' holds some tasksets for testing, 'loggingMonitor.py' is a [Monitor](monitor.md) for testing, which writes to logs/monitor.log)



    from test import example5
    from distributor.distributorClass import Distributor
    from distributor.monitors.loggingMonitor import LoggingMonitor


Defining a monitor and tasksets for the execution is left to the user.


**Initialize modules:**



    t = example5()
    lm = LoggingMonitor()
    dist = Distributor()


Now the distributor is running.

**Adding a job** is possible via the add_jobs([taskset], monitor) function: 

   

    dist.add_job([t],lm)


This will spawn machines acording to the current max_machine value.


Note: You can repeat the above command to queue multiple jobs whenever you please.


To view a list of detached qemu instances 

    sudo screen -ls

To kill a detached screen type:


    sudo screen -X -S <name\_of\_screen> kill


The log files of the genode instances are also saved in the distributor/log/ directory.


Additionally, you can adjust the number of spawned machines, also while the distributor is running. See the distributor functions for more information. 







## Distributor functions

Setting max machines to a value between 1 and 42. You can change this anytime as this only affects the maximum total number of spawned machines. If machines are active, the number will be adapted accordingly. Closing machines will still finish their current taskset before shutting down. (The argument "max_allowed" can be passed in the Distributors init() to adjust the limit.):


        set_max_machine_value(numMachines)




Function to check if the distributor is busy or not:

        get_distributor_state()



Return current maximum value of possible active machines:


        get_max_machine_value()


Creating a new job and adding it to a list of jobs to be worked on.
The function is instantiating a new object of type \_Job which is then appended to the list of jobs to be processed:
 
        add_job(tasksetList, monitor=None, offset=0, *session_params)


A job always consists of list of TaskSet tasksetList and a Monitor implementing AbstractMonitor from monitor.py, the session\_parameters are optional. Inside the method a \_Job() will be created to hold the iterator over the list.


Kill all machines that are currently running **without** waiting for current tasksets to finish:


        kill_all_machines()

Stop all machines after they finished the execution of their current taskset:

        shut_down_all_machines()

Resume stopped machines:

        resume()

## The Machine class

The 'machine.py' implements a class which extends threading.Thread.

An instance of Machine is taking care of spawning a host, creating a session which connects to the spawned host and acquiring tasksets while there still is work to be done.

