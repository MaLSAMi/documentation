# Distributor 

Distributor is the main class/entity that controls and distributes host sessions to manage tasksets. Upon startup, the distributor will have a preset value of one host session that it will be able to spawn. The user is permitted to change this number at any time up to a hardcoded limit of seven. Machines set to be closed will finish their assigned taskset before being shut down. The distributor is mainly used for gathering large-scale data about autonomous system schedulability-tasks, which can be used for data mining and analysis. 



## Set up and Configuration

A vagrant script is provided in the client-tools repository, which will set up the appropriate development environment and prepare it for use without any manual installation or configuration. However, if you would like to configure your host machine manually, follow the steps below:

Clone the client-tools repository and initialize the submodules and place a working image.elf file inside the client-tools directory.


Install Python 3.5


    sudo apt-get install python3.5 -qq


Install bridge functionality for networking:


    sudo apt-get install bridge-utils -qq


Download DHCP service and move provided configuration file. 


    sudo apt-get install nmap isc-dhcp-server -qq
    sudo cp dhcpd.conf /etc/dhcp/
    
Set up the bridge and assign an IP address (consult the dhcp.conf file for more information on IP ranges)


    sudo brctl addbr br0
    sudo ip addr add 10.200.40.1/21


Adjust /etc/network/interfaces file with preliminary networking information


    sudo sh -c 'echo "auto br0\niface br0 inet dhcp\nbridge_ports eth0\nbridge_stp off\nbridge_maxwait 0\nbridge_fd 0\n" >> /etc/network/interfaces'


Install qemu and screen for spawning host sessions from the distributor and for easy visualization of spawned sessions. 


    sudo apt-get install qemu -qq
    sudo apt-get install screen -qq

Start the dhcp service

    sudo systemctl start isc-dhcp-server

The machine should now be ready for use. Let's start the distributor now. 

Open up the interactive python shell in the directory of the distributor_service (You can also create and execute this in a script)


    sudo python3



Add appropriate imports ('example.py' holds some tasksets for testing. Also 'loggingMonitor.py' is a monitor for testing, which writes to distributor_service/logs/monitor.log You are welcome to use your own classes.)



    from example import Hey0TaskSet
    from monitors.loggingMonitor import LoggingMonitor
    from distributor import Distributor




Initialize modules



    t = Hey0TaskSet()
    lm = LoggingMonitor()
    dist = Distributor()


Now the distributor is running.

Adding a job is possible via the add_jobs() function: 

   

    dist.add_job(t,lm)


This will trigger another function in which machines will be spawned acording to the set max_machine value.


Note: You can repeat the above command to queue multiple jobs whenever you please. 

To view a list of detached qemu instances 

    sudo screen -list

To reatach to for example the screen with the name 'qemu1'

    sudo screen -xr qemu1




In a separate shell, you can trace the execution of the distributor by tailing the log file




    tail -f log/distributor.log





7.Additionally, you can adjust the number of spawned qemu instances, max number of host machines, also while the distributor is running. See the distributor functions for more information. 







## Distributor functions

Setting max machines to a value between 1 and 7. You can change this anytime as this only affects the maximum total number of spawned machines. If machines are active, the number will be adapted accordingly. Closing machines will still finish their current taskset before shutting down.


        set_max_machine_value(numMachines)




Function to check if the distributor is working or not. 

        get_distributor_state()



Return current maximum value of possible active machines


        get_max_machine_value()


Creating a new job and adding it to a list of jobs to be worked on.
The function is instantiating a new object of type TaskSetQueue which is then appended to the list of jobs to be processed.
 


        add_job(taskset, monitor, *session_parameters)

A job always consists of Taskset t and a Monitor, the session\_parameters are optional. TaskSetQueue will hold the iterator which is returned by t.variants()

Kill all machines that are currently running 


        kill_all_machines()



## The Machine class

The 'machine.py' implements a class which extends threading.Thread.

An instance of Machine is taking care of spawning a host, creating a session which connects to the spawned host and acquiring tasksets while there still is work to be done.

## The Monitor component

The provided monitor 'mon' has to implement the AbstractMonitor as defined in distributor\_service/monitor.py

Everytime after a taskset finished execution

    mon.__taskset_finish__(self, finished_taskset)

is called. This is the function which should write data into a database of some kind.

    mon.__taskset_stop__(self, running_taskset)

is called if a taskset was not finished but the machine could not finish the current set. This method should clear the jobs attribute of every task in the set.  