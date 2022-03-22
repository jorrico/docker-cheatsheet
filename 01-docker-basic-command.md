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
5. `-e ENV_VARIABLE=ENV_VALUE`

### [Stopping Running Container](https://docs.docker.com/engine/reference/commandline/stop/)

    $ docker stop [OPTIONS] CONTAINER [CONTAINER...]

### [Rerun Stopped Container](https://docs.docker.com/engine/reference/commandline/start/)

    $ docker start [OPTIONS] CONTAINER [CONTAINER...]

### [Show All Initialized Containers](https://docs.docker.com/engine/reference/commandline/ps/)

    $  docker ps [OPTIONS]

Some useful `OPTIONS`:
1. `-a`

---
## Debugging a Container

### [Pulling Logs](https://docs.docker.com/engine/reference/commandline/logs/)

    $ docker logs [OPTIONS] CONTAINER

Some useful `OPTIONS`:
1. `-f`

### [Starting Interactive Terminal Session](https://docs.docker.com/engine/reference/commandline/exec/)

    $ docker exec [OPTIONS] CONTAINER COMMAND [ARG...]

Some useful `OPTIONS`:
1. `-it`

Some useful `COMMAND`s:
1. `docker exec -it CONTAINER /bin/bash`

---
## Networking in Docker

### [Command for Networking](https://docs.docker.com/engine/reference/commandline/network/)

    $ docker network COMMAND

Some useful `COMMAND`s:
1. `ls`
2. `create NETWORK-NAME`

---
### [Shortening `docker run` Command](https://docs.docker.com/compose/reference/)

Running `docker run` with multiple configuration can be a little tedious. This is where `docker-compose` comes into picture. The command `docker-compose` takes `.yml` file to create container from image. The following command

$ docker run p 8081:8081 -e SPARK_WORKER_CORES=1 -e SPARK_WORKER_MEMORY=512m --name spark-worker-1 --volumes shared-workspace:/opt/workspace andreper/spark-worker:3.0.0

can be done using `docker-compose` on the following `.yml` file:

```
version:'3'
services:
    spark-worker-1:
        image: andreper/spark-worker:3.0.0
        container_name: spark-worker-1
        environment:
            - SPARK_WORKER_CORES=1
            - SPARK_WORKER_MEMORY=512m
        ports:
            - 8081:8081
        volumes:
            - shared-workspace:/opt/workspace
```

Multiple services (**Read: Containers**) can be bundled in a single `.yml` file so that those containers run together ([example](https://github.com/cluster-apps-on-docker/spark-standalone-cluster-on-docker/blob/master/docker-compose.yml)). Docker automatically creates a network so we don't need to run `docker network create NETWORK-NAME` for it.

To run using `.yml` file, use the following command:

    $ docker-compose [-f <arg>...] [--profile <name>...] [options] [COMMAND] [ARGS...]

If `-f FILENAME` is not provided, it will look for `docker-compose.yml` file.

To shut down containers, either use `docker stop` or `docker-compose -f FILENAME down`. Good thing is, `docker-compose down` stops network