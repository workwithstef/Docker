# Docker Lets Go!

## Common Commands

### Basics

`docker version` - shows version installed and client/server versions running on local machine (highlights virtual linux running on windows kernel)

`docker info` - shows active/inactive containers

`docker run <image_name>` - starts container based off image

docker run process:

- Docker client contacts Docker daemon checking for <container_name> image locally
- if not available locally, daemon pulls image from DockerHub repo
- uses that image to create a new copy of the container


### Images

`docker images` - lists all active images (option `-q` shows only image id)

`docker pull <image_name>` - copies image to Docker host filesystem

`docker rmi <imageID>` - removes image

### Containers

`docker ps -a` - shows all running (& previously running) docker containers

`docker stop/start <container>` - stops/starts containers

*containers are persistent; will restart with all the same data until it is forcibly removed with `docker rm <container>`*

`docker run -d --name <name_for_container> -p <from-port:to-port> <DockerHub_repo/image_name>` - more intricate container start

(option `-d` = container will run in the background)
(`--name <name_for_container>` = gives the copied image a new name as a running container)
(`-p <from-port:to-port>` = used for *mapping ports*. If the container is a web server running on port 8080 & you want to access it from port 80, then "-p 80:8080")
(`<DockerHub_repo/image_name>` = specified path for image)

`docker run -it <container>` - runs container and logs into subsequent terminal. (i.e. ubuntu shell)

### System

`docker stats` - mem usage, general container info
`docker system df` - disk usage info for Docker





## Latest Docker Features

### Swarm Mode (Docker v1.12 or later)


- a swarm == a native cluster of docker engines

- a running swarm is called 'swarm mode'

- manager nodes maintain the swarm; highly available nodes - usually 3 or 5 manager nodes

- only one leader.

- Manager nodes instruct worker nodes.

- worker nodes execute tasks.

*managers also act as workers by default*

- Services = declarative way of running tasks

e.g. an app with a web front-end interface & and back-end infrastructure counts as 2 services. With Docker Services you can tell docker to create the web front-end service on a set no. of instances, and the workers will make sure that is maintained.

`docker service create --name web-fe --replicas 5`

*will create 5 instances of web-fe*

- Tasks - assigned to workers; essentially containers

### Building a Swarm

Prereqs:

- Have 6 instances running Docker (AWS instances/VMs/6 servers on-prem)

The Plan:
- 3 manager nodes, 3 worker nodes
- initialise the 1st manager nodes, then join two more managers.
- then join the 3 remaining workers

[within 1st node]

- `docker version` - make sure running v1.12 or higher
- `docker swarm init --advertise-addr {IP} --listen-addr {IP}` - initialises swarm; '--adv-addr {IP}' no matter how many IPs the instance has, this is the IP which does swarm mode; 'listen-addr {IP}' sets the IP which this IP listens to

*native docker ports: Engine port - 2375; Secure Engine port - 2376; Swarm port - 2377.*

- `docker swarm join-token manager` - produces unique token key, used to add manager node

- `docker swarm join-token worker` - produces unique token key, used to add worker node

[within other managers]

- copy and paste required join command + '--adv-addr {currentIP} --listen-addr {currentIP}' to keep IP persistent.

[within workers]

- copy and paste required join command + '--adv-addr {currentIP} --listen-addr {currentIP}' to keep IP persistent.

[within manager nodes]

- `docker node ls` - shows active node info; incl. manager status

- `docker node promote {ID}` - promotes worker node to manager node

### Services

`docker service create --name psight1 -p 8080:8080 --replicas 5 nigelpoulton/pluralsight-docker-ci` - creates service, 5 instances based on container, listening on port 8080, named "psight1".

`docker service ls` - shows active services

`docker service ps psight1` - shows running processes

`docker service inspect psight1` - shows config of service
