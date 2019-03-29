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
If you simply want to test the setup inside a small vagrant machine, type:
```bash
make
```
this will take a while, but leave you inside a vagrant machine, here you can go to the distributor component and run a test program.
```bash
cd /vagrant/distributor/
sudo python3 test.py
```


If you only want to build the operating system including the binaries