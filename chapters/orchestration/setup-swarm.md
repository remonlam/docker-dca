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
Open a terminal and ssh into the machine where you want to run your manager node. This tutorial uses a machine named manager1. If you use Docker Machine, you can connect to it via SSH using the following command;

But the first step is to retrieve the IP address of master1;

``sh
$ docker-machine ls | grep master1
``

``sh
$ docker-machine ssh manager1
``




Run the following command to create a new swarm;
docker swarm init --advertise-addr <MANAGER1-IP>



# Add a second Swarm Manager


# Add multiple Worker Nodes


# What you have learned
