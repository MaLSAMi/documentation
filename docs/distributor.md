# Overview of Modules

Distributor is the main class/entity that controls and distributes host sessions to manage tasksets. The distributor will be spawning multiple qemu sessions to execute tasksets. The qemu sessions will be waiting for events from the Gnode session. 

Requirements:

Networking capabilities (dhcp,bridge,tap,...)


## Set up and Configuration

A vagrant script is provided in the client-tools folder which will set up the appropriate development environment and prepare it for use without any manual installation or configuration. However, if you would like to configure your host machine manually, follow the steps below:


Install bridge functionality for networking:



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


Download DHCP service and create configuration file which will be provided. 


    sudo apt-get install nmap isc-dhcp-server -qq
    sudo cp /vagrant/dhcpd.conf /etc/dhcp/
    sudo apt-get install htop -qq


Set up the bridge and assign an IP address (consult the dhcp.conf file for more information on IP ranges)


    sudo brctl addbr br0
    sudo ip addr add 10.200.40.1/21


The machine should now be read for use!


1. Start DHCP Server with (Enter command here)

2. Start up distributor 

3. Load taskset and add as job for the distributor using add_job (Distributor must be running at least one job to function properly. (Gnode ignores any case with 0 jobs)

Example:

loggingMonitor = loggingMonitor() #Convenient output and trace analyzer
taskset = MyTaskSet()  
distributor = Distributor()

dist.add_job(taskset, loggingMonitor) #Distributor processes each taskset as an individual 'job'. You can add as many job as you would like as long as you have at least one. 


## Modules 

Distributor


## Distributor Functions

"""Setting max machines to whichever value you would like. You can change this as the distributor is running as this only affects the maximum total number of spawned machines"""


set_max_machine_value(numMachines)

Function to check if the distributor is working or not. 

get_distributor_state()

get_max_machine_value

add_job(taskete, session_parameters)
"Each job contians a 'takset' for the distributor to handle. "


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
