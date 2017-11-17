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

```
$ docker-machine ls

NAME   ACTIVE   DRIVER   STATE   URL   SWARM   DOCKER   ERRORS
```

## Create new master VM;
Next step is to create a new master instance, named 'master1';

```
$ docker-machine create --driver virtualbox master1
...

Running pre-create checks...
Creating machine...
(master1) Copying /Users/user/.docker/machine/cache/boot2docker.iso to /Users/user/.docker/machine/machines/master1/boot2docker.iso...
(master1) Creating VirtualBox VM...
(master1) Creating SSH key...
(master1) Starting the VM...
(master1) Check network to re-create if needed...
(master1) Waiting for an IP...
Waiting for machine to be running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH to be available...
Detecting the provisioner...
Provisioning with boot2docker...
Copying certs to the local machine directory...
Copying certs to the remote machine...
Setting Docker configuration on the remote daemon...
Checking connection to Docker...
Docker is up and running!
To see how to connect your Docker Client to the Docker Engine running on this virtual machine, run: docker-machine env master1
```

## Create other Docker instances;
Repeat the previous step for each of the following names: "master2", "worker1" and "worker2".

When all instances has been successfully created the output of docker-machine should look like the following example;

```
$ docker-machine ls

NAME      ACTIVE   DRIVER       STATE     URL                         SWARM   DOCKER        ERRORS
master1   -        virtualbox   Running   tcp://192.168.99.100:2376           v17.10.0-ce   
master2   -        virtualbox   Running   tcp://192.168.99.101:2376           v17.10.0-ce   
worker1   -        virtualbox   Running   tcp://192.168.99.102:2376           v17.10.0-ce   
worker2   -        virtualbox   Running   tcp://192.168.99.103:2376           v17.10.0-ce
```

## Access the VM's;
In order to get console access the virtual machines we can use docker-machine ssh command, like the following example.

```
$ docker-machine ssh master1

                        ##         .
                  ## ## ##        ==
               ## ## ## ## ##    ===
           /"""""""""""""""""\___/ ===
      ~~~ {~~ ~~~~ ~~~ ~~~~ ~~~ ~ /  ===- ~~~
           \______ o           __/
             \    \         __/
              \____\_______/
 _                 _   ____     _            _
| |__   ___   ___ | |_|___ \ __| | ___   ___| | _____ _ __
| '_ \ / _ \ / _ \| __| __) / _` |/ _ \ / __| |/ / _ \ '__|
| |_) | (_) | (_) | |_ / __/ (_| | (_) | (__|   <  __/ |
|_.__/ \___/ \___/ \__|_____\__,_|\___/ \___|_|\_\___|_|
Boot2Docker version 17.10.0-ce, build HEAD : 34fe485 - Wed Oct 18 17:16:34 UTC 2017
Docker version 17.10.0-ce, build f4ffd25
docker@master1:~$
```
