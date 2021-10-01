# Docker: The Big Picture

## Containers: Primer

Bad days = overpowered servers not operating to their capacity >>> VMware = Maximize server capacity buy configuring VMs to be as powerful as needed

Each VM runs ONE app (e.g app/db/aws/etc).

each VM uses a slice of the main server's power, they each have a dedicated OS; which uses a large chunk of resources (CPU/disk space)
+ OS overheads (licensing costs, admin, updates, etc.)
BIG WASTE hence ==> Containers

What is a Container?

Instead of having multiple VMs each with their own OS, we have ONE OS. Then we have one container per app - each container is a slice of the OS.
-- Containers are smaller and more efficient than VMs --
Apps start faster since the collective OS is already running
-- OS-specific apps only run on Dockers with specific OS --



## Docker

- Docker, Inc.
- Docker Project

Docker makes containerization of apps easy.

Steps:
- take the app source code
- build a Docker image based on the source code
- source code now packaged to be used as a container
- push image to a registry i.e. DockerHub
- Run Docker container


## Kubernetes (K8s)

- available on all good cloud platforms
- available on-premises
- available on laptop dev-environments
- extremely extensive

What does it do?

Essentially the scaling side of Docker containerization.

Kubernetes cares about HOW MANY containers to start/stop, can update containers without downtime

it can act as a load balancer and scale up more apps when nodes are overloaded.

Specifically, each node (on-prem/Cloud platform) has a Kubernetes agent. Above the node level there is a k8s 'master controller' which decides what to run on what node (i.e. the app on node 2 & the db on node 3). If node 2 is overloading then k8s can automatically spin up another container on a different node - load balancer style.

K8s can also easily migrate your apps between cloud platforms & on/off cloud.

## Thriving in a Container World

### individual preparations
- get your hands dirty!!! play with Docker/Kubernetes
- www.play-with-docker.com
- www.play-with-k8s.com
- Docker Desktop
- plural sight - get learning

### organisational preparations
- containers are coming...
- check if your organsation are already using Containers
- set up a team of developers to work on a special project which requires extensive use of docker/k8s
- Get people hyped and tell them all about it; encouraging use throughout the company, hence not being late to the party



## Suitable Workloads

- Stateful = has to remember stuff

E.g. if a DB goes down, it HAS to come back up with all up-to-date data
- Stateless = doesn't remember stuff. nothing is stored.


## Enterprise & Production Readiness

### Is Docker Ready?
- community edition
- enterprise edition; better security, stability, steady releases etc.

### Is Kubernetes Ready?
- cloud services have their own hosted k8s services (AWS,Azure,Google)

- Alpha/Beta/GA stages

-Alpha used for early code, off by default, not for Production

-Beta; becoming stable

-GA for production, stable

## Orchestration

How everything comes together and is managed.

Different aspects of app architecture; web front-end, DBs, load balancers, APIs, etc.

K8s is the orchestrator which manages the combined different aspects of app architecture.
