# What is Docker?

A Platform for consistently building, running, and shipping applications.


    ## pros

        ##Application will work same as it's working on other machine.

# Problem Before Using Docker

1. Versioning issue.
2. One or more files missing.
3. "Different configurations settings across platforms."


##  With Docker we can package our application and run it anywhere on any machine with docker.


## As Docker run independently so we can remove when every we wan to remove the images as it is not in use.

 - docker-compose down --rmi all
 

# Note

- On windows we can run windows + linus containers.
- On Linux machine we can run linux containers.


# Containers vs VM

1. An isolated environment running an application whereas VM is running on a physical machine.
    -> Means VM needs to have a copy of OS whereas Container doesn't it share same Host os more accuratly share's't.

What is Image?

- Docker file contains all info about what things is needed by the project to get upend running. These requirements or package are 
    present inside container in form of images.

    for example - 
    a container have image of python, node, anything else.


## Our application is loaded inside the container.
## To run any project instead of normal way we can use docker to run it
- command to up

```
docker-compose up
```

- command to down
```
docker-compose down
```

- to run it in background

- use
  
```
docker-compose up/down -d
```


And we can push image to Docker registry (just like git/github)
we can push that image to make it available to use by others.



# Now for example (uploading an image)-

- create a file any js/python/ruby/dart

1. Start with os (in my case it is Linux)
2. Install Python
3. Copy app files
4. Run day1.py file

Run 

```
docker build -t beginner-tutorial .
```

-t means tags
. means current directory

> **NOTE - beginner-tutorial is tag name (you can use other)**

Now to view the images

```
docker image ls
```

NOTE - in Dockerfile
you can define the distribution you want like

FROM  python:apline

Now to run the docker image

docker run image-name


To get image from local 

# docker run ubuntu 

""Docker will check whether the image is locally present if yes use
else pull from DockerHub.""


# To check running process or running containers use

- docker ps

# To check stop container as well 

- docker ps -a

# To start a container and interact with it

- docker run -it image-name

-it means iteractive terminal

# To get inside running container

- docker exec -it <mycontainer> bash

example -

run docker image in interactive terminal

sudo docker run -it beginner-tutorial


# create image 

example 

sudo docker tag beginner-tutorial vishalyadav28/beginner-tutorial

# push -

example

sudo docker push vishalyadav28/beginner-tutorial

#updated Aug 24


### remove/stop all containers

- docker rm $(docker ps -aq)

- docker stop $(docker ps -aq)


rm means remove 
ps means containers
-a means all
-q means display only ids

### remove all images

- docker rmi $(docker image -q)


rmi means remove the images
-q means get the image ids



#=========================================================#

# Docker compose


# JSON(Javascript object notation)

{
    "name":"nobody",
    "roles": ["developer","superadmin"],
    "info": {
        "firstname":"no",
        "lastname":"body"
    }
    
}


# YAML              #starts with three hypens

---

name: nobody
roles:
    - developer
    - superadmin
info:
    firstname: no
    lastname: body

#let's create docker-compose file 




#Updating date June 25 2024

**Some important topic Docker**

- **Docker layering**
 when we define docker-compose file then that's called layering.

- Best practice is to define single process in a container.

- The Docker daemon (dockerd) is the core component that manages Docker containers, images, networks, and storage volumes.

- To provide a name to the container
    docker run -it --name container_name any_container

- **PORT Mapping:**
    Exposing the contaier at a praticular port so that it can be accessed outside the container.

- **Environment variable:**
    **example** - 
    ```docker run --name my_custom_container -e MY_ENV_VAR=value -d nginx```

```
      docker-compose up -d
     -d means detachable mode
```

- **Docker Networking:**

    1. Bridge (default)
    2. Host
    3. none
    3. overlay
    4. ipvlan
    5. macvlan

- **Bridge Network**
    Bridge Network is the default network mode for Docker containers.
    Containers on the same bridge network can communicate with each other using their container names.
    To expose a container to the outside world (i.e., to access it from your host or another network), you need to map the container’s ports to the host’s ports using the -p or --publish option. For example, -p 8080:80 maps     port 80 in the container to port 8080 on the host.
    This means you need to explicitly expose specific ports if you want to access container services from outside the Docker host.
- **Host Network**
    Host Network mode makes the container use the host’s networking stack.
    In this mode, the container shares the network namespace with the host, so there is no need to map ports explicitly. The container’s services will be accessible on the same IP address as the host.
    For example, if a container is running a web server on port 80 and you use --network host, the web server will be accessible on port 80 of the host’s IP address.
    This can be more efficient for networking performance, but it comes with less isolation between the container and the host.

  **Summary**

- **Compare Bridge and Host :**

    Bridge Network requires exposing containers on specific ports using port mappings.
    Host Network does not require explicit port mapping because the container shares the same network as the host.
    Here’s a corrected version of your statement:
    
#

> "Bridge network mode requires exposing containers on specific ports, but host network mode does not, as it uses the same network stack as the host system."
    
#

3. **None:**

    Completely isolate a container from the host and other containers.
   
    **for example -** 

    ```
        docker run -it network=none container
    ```
   > till now if you will ping the container using host and bridge it will return something...but in case of newtork=none it means you have disconnected the container from other and host also so it will run isolated.

## Creating own network and connecting that with the multiple containers:

Step 1:
- create a network:
```
docker network create -d bridge network_name
```
Step 2:
- create container1 using that network:
```
docker run -it --network=youtube --name container1 ubuntu
```
- create container2 using that network:
```
docker run -it --network=youtube --name container2 busybox
```
Step 3:
- You can ping one conatiner with other but container must be running...


