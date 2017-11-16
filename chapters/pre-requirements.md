# Setting up your lab environment

## What do we need to do;
- [Installing Docker](# Installing Docker)
- Create the first Swarm Manager
- Add a second Swarm Manager
- Add multiple Worker nodes
- What you have learned

# Installing Docker
Because you're os most likely does not include Docker we need to install it.
Go to the Docker website to download the installer;
- Mac users: https://www.docker.com/docker-mac
- Windows users: https://www.docker.com/docker-windows

Detailed installation guide can be found in the Docker Store;
- Mac - https://store.docker.com/editions/community/docker-ce-desktop-mac
- Windows - https://store.docker.com/editions/community/docker-ce-desktop-windows


# Installing VirtualBox
Because we need more than one instance of Docker and the easies way to get this is using docker-machine.
However docker-machine does not have a hypervisor we need to install one, in this example we are using the free VirtualBox.

Go to the VirtualBox website (https://www.virtualbox.org) and download the installation sources;
- Mac - http://download.virtualbox.org/virtualbox/5.2.0/VirtualBox-5.2.0-118431-OSX.dmg
- Windows - http://download.virtualbox.org/virtualbox/5.2.0/VirtualBox-5.2.0-118431-Win.exe

# Create lab VM's with Docker-Machine
Once VirtualBox has been installed we could check if docker-machine is able to create a VirtualBox VM.

First check if there is already something running (this should not be the case)

```sh
$ docker-machine ls

NAME   ACTIVE   DRIVER   STATE   URL   SWARM   DOCKER   ERRORS
```

## Create new master VM;
Next step is to create a new master instance, named 'master1';

```sh
$ docker-machine create --driver virtualbox master1
```
