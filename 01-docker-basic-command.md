# Yet Another Docker Cheatsheet
From: [TechWorld with Nana](https://youtu.be/3c-iBn73dDE)

---
## Container VS Image
Container is a running environment for image. Container consists of but not limited to:
1. File system (virtual)
2. Environment configs
3. **Application images**

Example of images:
1. Postgres
2. Redis
3. Mongo
4. Custom images

Container has a port that enables us to communicate with applications

---
## Important Commands

### [Pulling an image](https://docs.docker.com/engine/reference/commandline/pull/)

    $ docker pull [OPTIONS] NAME[:TAG]

### [Getting images info](https://docs.docker.com/engine/reference/commandline/images/)

    $ docker images [OPTIONS] [REPOSITORY[:TAG]]

### [Starting a Container With an Image](https://docs.docker.com/engine/reference/commandline/run/)

    $ docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

Some useful `OPTIONS`:
1. `-d`
2. `-pXXXX:YYYY` where `XXXX` and `YYYY` respectively are host and container IP
3. `--name NAME`
4. [`--net NETWORK-NAME`](#networking-in-docker)

### [Stopping Running Container](https://docs.docker.com/engine/reference/commandline/stop/)

    $ docker stop [OPTIONS] CONTAINER [CONTAINER...]

### [Show All Initialized Containers](https://docs.docker.com/engine/reference/commandline/ps/)

    $  docker ps [OPTIONS]

Some useful `OPTIONS`:
1. `-a`

---
## Debugging a Container

### [Pulling Logs](https://docs.docker.com/engine/reference/commandline/logs/)

    $ docker logs [OPTIONS] CONTAINER

### [Starting Interactive Terminal Session](https://docs.docker.com/engine/reference/commandline/exec/)

    $ docker exec [OPTIONS] CONTAINER COMMAND [ARG...]

Some useful `OPTIONS`:
1. `-it`

Some useful commands:
1. `docker exec -it CONTAINER /bin/bash`

---
## Networking in Docker

### [Command for Networking](https://docs.docker.com/engine/reference/commandline/network/)

    $ docker network COMMAND

Some useful `COMMAND`s:
1. `ls`
2. `create NETWORK-NAME`