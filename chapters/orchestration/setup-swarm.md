# Complete the setup of a swarm mode cluster, with managers and worker nodes

## What do we need to do;
- [Pre-requirements](#prereqs)
- Create the first Swarm Manager
- Add a second Swarm Manager
- Add multiple Worker nodes
- What you have learned

# Pre-requirements
Follow [this guide](../pre-requirements.md) to setup the lab environment.

# Create the first Swarm Manager
Open a terminal and ssh into the machine where you want to run your manager node. This tutorial uses a machine named manager1.<br>
If you use Docker Machine, you can connect to it via SSH using the following command;

### Get IP of master1
But the first step is to retrieve the IP address of master1;<br>
Remember the IP (without the port number) of master1 you need it later on.<br>
``sh
$ docker-machine ls | grep master1
``

### Connect with SSH to master1<br>
``sh
$ docker-machine ssh manager1
``


Run the following command to create a new swarm;<br>
Example: "docker swarm init --advertise-addr <MANAGER1-IP>"
``sh
$ docker swarm init --advertise-addr 192.168.99.100
``

### It should display something similar like this;
``sh
docker swarm init --advertise-addr 192.168.99.100


Swarm initialized: current node (y7ah4hw3zqqrqtyobry897o1k) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-1q7jja1jngryrtnsyk856g7z4658t24kjiv1751939uz22hfko-dk7um7zb6hzwiluzpovao84cy 192.168.99.100:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.
``

Make sure you copy the "docker swarm join" string.<br>
Example: "docker swarm join --token SWMTKN-1-1q7jja1jngryrtnsyk856g7z4658t24kjiv1751939uz22hfko-dk7um7zb6hzwiluzpovao84cy 192.168.99.100:2377"
# Add a second Swarm Manager



# Add multiple Worker Nodes


# What you have learned
