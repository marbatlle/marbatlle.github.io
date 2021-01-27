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
**Docker provides the ability to package and run an application in a loosely isolated environment called a container. The isolation and security allow you to run many containers simultaneously on a given host. Containers are lightweight because they don’t need the extra load of a hypervisor, but run directly within the host machine’s kernel. This means you can run more containers on a given hardware combination than if you were using virtual machines**

### Image