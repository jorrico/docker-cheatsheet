# Basic Docker Commands
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

1. [Pulling an image](https://docs.docker.com/engine/reference/commandline/pull/)

```
$ docker pull [OPTIONS] NAME[:TAG]
```

2. [Getting images info](https://docs.docker.com/engine/reference/commandline/images/)

```
$ docker images [OPTIONS] [REPOSITORY[:TAG]]
```

3. [Starting a Container for an Image](https://docs.docker.com/engine/reference/commandline/run/)

```
$ docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```