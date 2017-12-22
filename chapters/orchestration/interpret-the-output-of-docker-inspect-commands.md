# Interpret the output of docker inspect commands

## Inspect a service and get a more readable overview;

````
docker service inspect --pretty hello-ping

ID:		9uk4639qpg7npwf3fn2aasksr
Name:		hello-ping
Service Mode:	REPLICATED
 Replicas:		1
Placement:
UpdateConfig:
 Parallelism:	1
ContainerSpec:
 Image:		alpine
 Args:	ping docker.com
Resources:
Endpoint Mode:  vip
````

## Inspect a service and get a overview in JSON;

````
docker service inspect hello-ping

[
{
    "ID": "9uk4639qpg7npwf3fn2aasksr",
    "Version": {
        "Index": 418
    },
    "CreatedAt": "2016-06-16T21:57:11.622222327Z",
    "UpdatedAt": "2016-06-16T21:57:11.622222327Z",
    "Spec": {
        "Name": "helloworld",
        "TaskTemplate": {
            "ContainerSpec": {
                "Image": "alpine",
                "Args": [
                    "ping",
                    "docker.com"
                ]
            },
            "Resources": {
                "Limits": {},
                "Reservations": {}
            },
            "RestartPolicy": {
                "Condition": "any",
                "MaxAttempts": 0
            },
            "Placement": {}
        },
        "Mode": {
            "Replicated": {
                "Replicas": 1
            }
        },
        "UpdateConfig": {
            "Parallelism": 1
        },
        "EndpointSpec": {
            "Mode": "vip"
        }
    },
    "Endpoint": {
        "Spec": {}
    }
}
]
````

## Get detailed service information;

````
docker service ps hello-ping

NAME                                    IMAGE   NODE     DESIRED STATE  LAST STATE
hello-ping.1.8p1vev3fq5zm0mi8g0as41w35  alpine  worker2  Running        Running 3 minutes
````

### Show container info on local node;
When a container is running on a specific node it's possible to check if it's running.
Login to the host (in the example above it's "worker2").

````
docker ps

CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
e609dde94e47        alpine:latest       "ping docker.com"   3 minutes ago       Up 3 minutes                            hello-ping.1.8p1vev3fq5zm0mi8g0as41w35
````
