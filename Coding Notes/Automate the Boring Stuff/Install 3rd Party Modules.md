Python 3.4+ has pip tool to install 3rd party modules

Check pip installation with:
```
which pip3
```

Installation:
============
Debian/Ubuntu:
sudo apt-get install python3-pip

Fedora:
sudo yum install python3-pip


Install 3rd party modules:
=========================
On Windows call pip
On Linux call pip3
On Mac call pip3

Never use sudo when installing python modules

# To install module of specific version:
# The --user option installs to your home dir
pip install --user send2trash==1.5.0
pip install --user requests==2.21.0

# To install the latest version:
pip install --user send2trach

# To update to the latest version:
pip install --user -U send2trach