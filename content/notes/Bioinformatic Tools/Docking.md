---
title: Docker
linktitle: Docker
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  example:
    parent: Bioinformatic Tools
    weight: 2

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 2
---

Notes from the *Working with Containers: Docker & Docker Compose* course from Educative.io:

**Course Description**:In this course, you will learn the fundamentals of Docker such as containers, images, and commands. You’ll then progress to more advanced concepts like connecting to a database container and how to simplify workflows with Docker Compose. At the end, you’ll learn how to monitor clusters and scale Docker services with Swarm.

**Course Link**
The link: https://www.educative.io/courses/working-with-containers-docker-docker-compose


# The Notes

## 1. Docker Architecture
{{< figure library="true" src="docker.jpg" >}}

### Docker Definition
*Docker provides the ability to package and run an application in a loosely isolated environment called a container. The isolation and security allow you to run many containers simultaneously on a given host. Containers are lightweight because they don’t need the extra load of a hypervisor, but run directly within the host machine’s kernel. This means you can run more containers on a given hardware combination than if you were using virtual machines*

### Image
Docker provides the facility to create a custom image on top of the Linux kernel with your app and its libraries. The image is a blueprint of the container and the container is created from it.

For simplicity, if you take this from an object-oriented programming point of view, an image is a class, where all the requirements are defined and declared. A container is an instance of the image. These images are stored somewhere in the cloud and pulled as needed.

### Container
A container is an instance of an image, which simulates the required environment with the use of the Linux kernel packaged in it. In the diagram, you can see app B is enclosed in one container. Similarly, you can enclose the other two apps as well.

### Docker Ecosystem
* **Docker Registry:** Docker maintains all the images in the registry and they can be pulled from the registry too

* **Docker Hub:** This is the repository for all your custom-built images. Images can be pushed and accessed from the Hub

* **Docker Client:** The CLI tool used to interact with the Docker server

* **Docker Daemon:** The Docker server process responsible for pulling, pushing, and building the images. It is also used for running the container

### Download Docker for Linux
Followed this tutorial: https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04

## 2. Docker Fundamentals
### Layers - Building Blocks in Docker
As every image is built on top of Linux kernel, it has some common dependencies that can be reused by other images. Docker bundles these dependencies in one stack and these stacks are called layers.

Only the instructions RUN, COPY, and ADD create layers. Other instructions create temporary intermediate images and do not increase the size of the build.Docker caches these intermediate layers to speed up the image building process. 

### Docker Run - Accessing Containers

    $ docker pull \<images-name>:\<version> #pulls image from Docker registry
    $ docker run \<images-name>:\<version> #runs container from mentioned image
    $ docker ps #shows all running containers
    $ docker ps -a #shows all available containers
    $ docker exec #executes a command in a running container


**Meaning of each column for ps output:**
* CONTAINER ID: shows the unique ID of each container
* IMAGE: the image from which the container is created
* COMMAND: command executed in the container while starting it
* CREATED: the time the container was created
* STATUS: the current status of the container
* PORTS: if any of the container ports is connected to the host machine, it will be displayed here
* NAMES: this is the name of a container. If it is not provided while creating the container, Docker provides a unique name by default.

**Get back to the bash of any running container:**

    $ docker exec -it <container id/name> bash

**Exit a running bash container:**

    $ exit

### Docker Commit Images
Since we can use the container like a normal Linux machine, we can work in it exactly as we work in any normal Linux machine.

**Start and access the containers shell:**

    $ docker ps -a #check the first entry or the entry which cas bash in its command column; copy the container id
    $ docker start <container_id/name> #start the container
    $ docker exec -it <conatiner_id/name> bash #access the containers shell

To commit changes to the container and create a new image from it, we need to change something in a container. 

**Install nano:**

    $ apt-get update
    $ apt-get install vim nano

**Create a Python program and commit the changes, creating a new image:**

    $ nano todays_date.py
    Add and save: 
    from datetime import datetime
    print("Today's date is "+ datetime.utcnow().strftime("%Y-%m-%d"))
    $ exit #exit the bash
    $ docker commit -m "<commit message>" <container_id/name> <new_image_name>:<version> #commit the container
    $ docker images #see the images on our system

**Push your image to your Docker Hub account so that anybody can access it:**

    $ sudo docker login #login to your docker account
    $ sudo docker tag <image_name> <your_docker_hub_username>/<image>:<version> #user tag
    $ sudo docker push <your_docker_hub_username>/<image>:<version> #push image online

## Managing Data for Containers
 Whenever you create a container from an image, it creates a new container without any data except the image data. We created the date-project image, which is a very small image. It has only one project file which we created in the container file system. If the container is removed before committing the changes, we will lose the data. So, it is always good practice to separate your data’s file system from the container’s file system.

 Whenever a container is created, a file system is also created with it, which is a default Linux filesystem. Although Docker shares the OS’s kernel, there is a separation between file systems.

Most times, you need to access the host files in the container for faster access to data and while coding as well, because you cannot code, build, and then check your code.

Docker’s bind mount and volumes can be used in such cases.

    $ docker volume --help #to get the volume help
    $ docker volume create #to create a new volume
    $ docker inspect volume #to inspect the created volume
    $ docker run -v #to mount a volume

{{< figure library="true" src="docker2.jpg" >}}