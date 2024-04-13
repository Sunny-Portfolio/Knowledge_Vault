Python 3.4+ has pip tool to install 3rd party modules

Check pip installation with:
```sh
which pip3
```

### Installation:
---
Debian/Ubuntu:
```sh
sudo apt-get install python3-pip
```

Fedora:
```sh
sudo yum install python3-pip
```


### Install 3rd party modules:
---
- On Windows call pip
- mOn Linux call pip3
- On Mac call pip3

Never use sudo when installing python modules

##### To install module of specific version:
The --user option installs to your home dir
```sh
pip install --user send2trash==1.5.0
pip install --user requests==2.21.0
```

##### To install the latest version:
```sh
pip install --user send2trach 
```

##### To update to the latest version:
```sh
pip install --user -U send2trach
```