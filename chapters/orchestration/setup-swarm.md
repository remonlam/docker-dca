# Complete the setup of a swarm mode cluster, with managers and worker nodes

## What do we need to do;
- [Pre-requirements](../pre-requirements.md)
- Create the first Swarm Manager
- Add a second Swarm Manager
- Add multiple Worker nodes
- [What you have learned](#What you have learned)


#Pre-requirements
Follow [this guide](../pre-requirements.md) to setup the lab environment.


# Create the first Swarm Manager
Open a terminal and ssh into the machine where you want to run your manager node. This tutorial uses a machine named manager1.<br>
If you use Docker Machine, you can connect to it via SSH using the following command;

### Get IP of manager1
But the first step is to retrieve the IP address of manager1;<br>
Remember the IP (without the port number) of manager1 you need it later on.<br>
```
$ docker-machine ls | grep manager1
```

### Connect with SSH to manager1
```
$ docker-machine ssh manager1
```


Run the following command to create a new swarm;<br>
Example: "docker swarm init --advertise-addr <MANAGER1-IP>"<br>
```
$ docker swarm init --advertise-addr 192.168.99.100
```

It should display something similar like this;,<br>
```
docker swarm init --advertise-addr 192.168.99.100


Swarm initialized: current node (y7ah4hw3zqqrqtyobry897o1k) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-1q7jja1jngryrtnsyk856g7z4658t24kjiv1751939uz22hfko-dk7um7zb6hzwiluzpovao84cy 192.168.99.100:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.
```

### Get Worker token
To be able to add new Worker nodes to the existing Swarm, you need to have the token.<br>
Here's how to retrieve the token;
```
$ docker swarm join-token worker

To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-1q7jja1jngryrtnsyk856g7z4658t24kjiv1751939uz22hfko-dk7um7zb6hzwiluzpovao84cy 192.168.99.100:2377
```


### Get Manager token
To be able to add new Manager nodes to the existing Swarm, you need to have the token.<br>
Here's how to retrieve the token;
```
$ docker swarm join-token manager

To add a manager to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-1q7jja1jngryrtnsyk856g7z4658t24kjiv1751939uz22hfko-7gtmf2qj6roni0ibysx3xrne4 192.168.99.100:2377
```

NOTE: tokens for Manager & Workers are different!


### Verify node config
Verify that the node has been configured as manager.
```
$ docker node ls
```

It should output something like the following example;
```
$ docker node ls

ID                            HOSTNAME            STATUS              AVAILABILITY        MANAGER STATUS
y7ah4hw3zqqrqtyobry897o1k *   manager1             Ready               Active              Leader
```


# Add a second Swarm Manager
The first manager has been configured now it's time configure the second manager node.<br>
NOTE: For production use alsways use at least 3 Swarm Managers for redundancy, 2 manager nodes won't give you any failover capacity.<br>
      Please read this guid for more information regarding Swarm Manager HA setup.

### Connect with SSH to manager2
```
$ docker-machine ssh manager2
```

### Join node to the Swarm as a worker
```
$ docker swarm join --token SWMTKN-1-1q7jja1jngryrtnsyk856g7z4658t24kjiv1751939uz22hfko-dk7um7zb6hzwiluzpovao84cy 192.168.99.100:2377
```

It should output something like the following example;
```
$ docker swarm join --token SWMTKN-1-1q7jja1jngryrtnsyk856g7z4658t24kjiv1751939uz22hfko-dk7um7zb6hzwiluzpovao84cy 192.168.99.100:2377
This node joined a swarm as a worker.
```

Right now the node have been added to the Docker Swarm, however it does not have the Manager role.<br>
To do so execute the following commands;

```
$ docker swarm SWMTKN-1-1q7jja1jngryrtnsyk856g7z4658t24kjiv1751939uz22hfko-dk7um7zb6hzwiluzpovao84cy manager
```

# Add multiple Worker Nodes
The next step is to add some workers do the Swarm cluster.<br>
To do so we need to have the join-tokens from one of the managers.<br>

If you do not have save it somewhere you need to go to one of the Manager nodes.
```
$ docker-machine ssh manager2
```

The next step is to get the Swarm join token for Worker nodes.
```
$ docker swarm join-token worker
To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-1q7jja1jngryrtnsyk856g7z4658t24kjiv1751939uz22hfko-dk7um7zb6hzwiluzpovao84cy 192.168.99.100:2377
```

### Add a Worker node
Now we have the token we could add a Worker node to the Swarm cluster.
```
$ docker-machine ssh worker1
```

And run the join command that we just retrieved from manager2
```
$ docker swarm join --token SWMTKN-1-1q7jja1jngryrtnsyk856g7z4658t24kjiv1751939uz22hfko-dk7um7zb6hzwiluzpovao84cy 192.168.99.100:2377
```

This should output something similar like this.
```
$ docker swarm join --token SWMTKN-1-1q7jja1jngryrtnsyk856g7z4658t24kjiv1751939uz22hfko-dk7um7zb6hzwiluzpovao84cy 192.168.99.100:2377
This node joined a swarm as a worker.
```

Repeat this step for any remaining Worker nodes, like worker2.

### Verify Swarm cluster
Because we are on a Worker node we can't see or change the Docker Swarm configuration.<br>
When running the command to show all the Swarm nodes it will give you a error like;
```
$ docker node ls
Error response from daemon: This node is not a swarm manager. Worker nodes can't be used to view or modify cluster state. Please run this command on a manager node or promote the current node to a manager.
```

So once again we need to go to one of the two manager nodes.
```
$ docker-machine ssh manager1
```

And execute the command to get the current node configuration.
```
$ docker node ls
ID                            HOSTNAME            STATUS              AVAILABILITY        MANAGER STATUS
y7ah4hw3zqqrqtyobry897o1k *   manager1             Ready               Active              Leader
8u4dvwd4uzvagl4viylzaaqw0     manager2             Ready               Active              Reachable
a920b1hvlwoznwywq6aekir8f     worker1             Ready               Active              
g9pct1bk3gus13q0x7ql40fvw     worker2             Ready               Active              
```

You should see a total of 4 nodes, 2 of them have the manager role and the remaining have Worker roles.


# Lessons learned
Okey so you now have a working Swarm cluster consist of 2 Manager nodes and 2 Worker nodes, in a recap this is what we have learned.
- Create the first Swarm Manager node
- Retrieve the tokens for both the Managers and Workers
- Add a second Swarm Manager node
- Add Swarm Workers
- Verify the node status
