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