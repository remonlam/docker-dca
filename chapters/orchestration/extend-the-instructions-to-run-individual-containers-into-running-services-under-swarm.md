# Extend the instructions to run individual containers into running services under swarm

## Deploy a service to Docker Swarm;

````
docker service create --replicas 1 --name hello-ping alpine ping docker.com
````

## Check if the service has been created;

````
docker service ls

ID            NAME        SCALE  IMAGE   COMMAND
0bl4649cug4b  hello-ping  1/1    alpine  ping docker.com
````

## Get detailed information about the specific service;

````
docker service ps hello-ping

NAME                                    IMAGE   NODE     DESIRED STATE  LAST STATE
hello-ping.1.8p1vev3fq5bl0ma8g0as41w35  alpine  worker2  Running        Running 3 minutes
````
