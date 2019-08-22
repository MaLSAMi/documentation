# First Steps

To try our setup you first have to checkout the client-tools repo
```bash
git clone https://github.com/malsami/client-tools
```
from here on out you can use the Makefile in the client-tools repository.
Switch into the folder:
```bash
cd client-tools
```
## Test Setup (Vagrant)
If you simply want to test the setup inside a small vagrant machine, type:
```bash
make
```
this will take a while, but leave you inside a vagrant machine. 

Here you can go to the distributor component and run a test program.
```bash
cd /vagrant/distributor/
sudo python3 test.py
```

## Only Genode Image and Task Binaries

If you only want to build the operating system (for the target focnados_pbxa0) including the binaries execute
If you want another target adjust the parameter accordingly. The binaries can afterwards be found in the 'bin' folder.
```bash
make genode-init
make binaries OS-TARGET=focnados_pbxa9
```

## Local Execution

For local execution a dhcp server has to be setup which takes care of ip assignment.
If the execution applies Genode on Qemu instances sudo rights are necessary to create and remove the network interfaces.
If the execution uses Genode on real hardware, the boards have to be prepared accordingly and the images must be provided for them to fetch.
To setup the repository execute (adjust OS-TARGET accordingly)
```bash
make venv
make distributor-init
make genode-init
make binaries OS-TARGET=focnados_pbxa9
make datageneration
```
Then you can enter the venv by typing 
```bash
source malsami/bin/activate
```
You are now inside the venv within which the dependencies are ready to execute a programm like e.g. the main.py inside the datageneration.

