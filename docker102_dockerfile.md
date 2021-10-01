# Building Docker Images


1. Create Dockerfile 
2. Build image -- `docker build <path to Dockerfile location>` 
	option `-t <image_name:tag>` allows you to name image; tag=version, e.g. "1.0"
3. Run image to create container `docker run <image_name>`



## Dockerfile Syntax


Basic example syntax
```
FROM ubuntu

MAINTAINER workwithstef <stefan.okolo@outlook.com>

RUN apt-get update

CMD ["echo", "Hello World"]
```
- `FROM ubuntu` specifies base image. Docker will search locally, if not, pull from DockerHub
- `MAINTAINER` [optional] specifies image creator & contact info
- `RUN apt-get update` command executed during building of image
- `CMD` executed when creating container off image