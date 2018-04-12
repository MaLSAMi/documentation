# Distributor and other relevant Modules

Distributor is the main class/entity that controls and distributes host sessions to manage tasksets. Upon startup, the distributor will have a set value of host sessions that it will be able to spawn. The user is permitted to change this number at any time. Machines set to be killed will finish their assigned taskset before being killed. 

Machine is the entire class that represents the machine that is executing the tasksets. This class is responsible for creating the QEMU instance (connected to the provided bridge) with Genode, to sending tasksets while listening for events from Genode. 


Requirements:

Networking capabilities (dhcp,bridge,tap,...)


## Set up and Configuration

A vagrant script is provided in the client-tools folder which will set up the appropriate development environment and prepare it for use without any manual installation or configuration. However, if you would like to configure your host machine manually, follow the steps below:


Install bridge functionality for networking:



    cd client-tools
    sudo apt-get update -qq
    sudo apt-get install python3.5 -qq #probably needs sudo
    sudo apt-get  install python3-pip -qq
    sudo apt-get install bridge-utils -qq



Add appropriate imports to appropriate files 


    sudo sh -c 'echo "import sys\nsys.path.append(\"/usr/local/lib/python3.5/dist-packages/pynetlinux\")\n$(cat /usr/local/lib/python3.5/dist-packages/pynetlinux/__init__.py)" > /usr/local/lib/python3.5/dist-packages/pynetlinux/__init__.py'

Adjust /etc/network/interfaces file with preliminary networking information


    sudo sh -c 'echo "auto br0\niface br0 inet dhcp\nbridge_ports eth0\nbridge_stp off\nbridge_maxwait 0\nbridge_fd 0\n" >> /etc/network/interfaces'


Install qemu and screen for spawning host sessions from the distributor and for easy visualization of spawned sessions. 


    sudo apt-get install qemu -qq
    sudo apt-get install screen -qq


Download DHCP service and move provided configuration file. 


    sudo apt-get install nmap isc-dhcp-server -qq
    sudo cp dhcpd.conf /etc/dhcp/
    sudo apt-get install htop -qq


Set up the bridge and assign an IP address (consult the dhcp.conf file for more information on IP ranges)


    sudo brctl addbr br0
    sudo ip addr add 10.200.40.1/21


The machine should now be ready for use. Let's start the distributor now. 


Start DHCP Server with <Enter command here>

Open up the interactive python shell (You can also create and execute this in a script)


    cd distributor_service
    sudo python3



Add appropriate imports (We have provided an example taskset for you to use in the file 'example.py'. You are welcome to use your own)



    from example import Hey0TaskSet
    from monitors.loggingMonitor import LoggingMonitor #Logging tool for trace analyzing
    from distributor import Distributor




Initialize modules



    t = Hey0TaskSet()
    lm = LoggingMonitor()
    dist = Distributor()



Start a job 

   

    dist.add_job(t,lm)





Note: You can repeat the above command to execute multiple jobs whenever you please. However, at least 1 job must be executed for the distributor to work. 


To view the qemu instances 




    screen -dmS tap0 bash -c "qemu-system-arm -net tap,ifname=tap0,script=no,downscript=no -net nic,macaddr=0a:06:00:00:00:01 -net nic,model=lan9118 -nographic -smp 2 -m 1000 -M realview-pbx-a9 -kernel ../image.elf"




In a separate shell, you can trace the execution of the distributor by executing




    tail -f log/distributor.log





7.Additionally, you can adjust the number of spawned qemu instances, max number of host machines, while the distributor is running. See the distributor functions for more information. 







## Distributor functions

Setting max machines to whichever value you would like. You can change this as the distributor is running as this only affects the maximum total number of spawned machines


        set_max_machine_value(numMachines)




Function to check if the distributor is working or not. 

        get_distributor_state()



Return current maximum value of allowable active machines


        get_max_machine_value


Given a taskset and other data provided by the sessions class (optional), this will add the taskset to the TaskSetQueue. Then it will distribute the taskset by either spawning a new machine or assigning it to the current available machines running. Distributor must be running at least one job for it to be active. 


        add_job(taskete, session_parameters)


Kill all machines that are currently running


        kill_all

        

## Machine Functions





Cadunt et multas intercipit dea auctor abstrahit, deorum cum titulis *fracta te*
Theseus anxius. Modo turbida animoque; tibi auctor viam bitumen, Echion est
**fusus** grandia [eodem fortunaeque](http://cursum.io/levitate) canum ad
muneris. Coronae Meleagros dulcia.

## Olympo erat cinerem Palilibus et tamen illis

Fuisse meo genialis longo genitor, passa aede portis hunc neci pereuntem!
Liquefacta exactum quassasque accipe.

    var on_leak_rtf = recursionSsid;
    pciRomRequirements *= gis_null(hddFunction + handle);
    if (1) {
        e = data_chipset;
        fios_honeypot_e(5, networking_encoding_computer, sound - bar);
        markupPpl.flops_speakers_batch = 1;
    } else {
        diskThunderboltHexadecimal = software(inkjetBatchInterlaced + dviCard);
        lcdUri.barebones.worm_plug(ntfsHashtag);
    }

Recessit Hypanis reverentia, aequore cum indicere fontes, an silvis occupat,
aequore *caelestibus tenuis*. Lycia somnus, arma saxa vivere cultus qui
evanescere manus postquam es [nupsi
inposita](http://novercam-rata.io/aderat-generosi.html) Thyoneus vellent quo
consorte. Augurium coniunx moenibus hostibus et matrum agros. Conplexa erat
crimen longis resonant fumabat fuerat. Ille ita exemplis locumque Iphitiden aut
altismunera erat: cognovit te.
