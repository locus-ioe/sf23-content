---
title: "Day 10: Containarizing our Project"
date: 2022-07-09
tags: []
draft: false
weight: 10
---

## Slides link [**link**](https://docs.google.com/presentation/d/1bTl---Bi3sT4NqAMeKOfJfRLLIb8LnIWpaksLjXoF3c/edit?usp=sharing)
## Github link [**link**](https://github.com/ankitpaudel20/sf23_django_lastday_docker)

# Containers

## Introduction

If you have been doing web development or programming in general, chances are you’ve already heard of containers or at least Docker. However without having to realize its importance, it doesn’t make sense to use them and understand them.

Imagine if you need to build project with Django version 3.6 for one application. You install the package through godly python tool called pip. `pip install django==3.6` But when you need to develop another application with version 4.0 you need to upgrade or uninstall and install django module. The problem is that, this only satisfies the requirements for one project at a time. Hence containers and other solutions come to the rescue. However we will logically prove how containers are more favorable than other solutions.

A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another. In a way it works similar to virtual machines but not quite. Now what container does is for those two django application project discussed above, it creates different environments with different specifications. In this way, it increases flexibility and portability.

## Why not Virtual Env?

As mentioned above, there are many other solutions to the problem. Python provides out of the box virtual environment called as venv which has been discussed in previous modules as well. Other python virtual environment is Anaconda which is popular amongst data science and machine learning enthusiasts.

However the problem with python specific virtual environment are very clear, it only works for python application. What happens when you want to glue golang and python code together in your project? You might think of maintaining separate environment: one for python using venv and another different tool for managing golang. This is difficult to maintain. Thats why containers come as a solution to tackle these specific problems.

## VMs vs Containers

Programmers back in the days, used to manage different VMs to program applications with different requirements. VMs isolate the programs completely. But if you’ve ever tried to spin up VMs with a image, you know it is very slow at bootup. Not only that, it takes separate space and has much more processing overload. In first glance, Containers and VMs seem like same technology, but containers only runs on base kernel and limited userspace while VMs has full fledged operating system. This figure below shows some relief some comparision:

Dont worry about all these terms used. These will not be used at all, however you’ll understand how layers of Container is formed later.

![docker vs vms.png](/attachments/docker_vs_vms.png)

## Docker

Docker is a set of PaaS (Platform as a Service) products as opposed to IaaS (VMs). Now what does that mean? It means that there are different services run by Docker. The one that we are interested in right now is Docker Engine and we will talk about other services as well briefly. Docker Engine is essentially a ship docking containers hence the name. Meaning it manages and hosts containers. One can reference the image from above to make clear of what Docker does there. These binaries and libraries that we see are managed in a file called Dockerfile. Application that is to be containarized should be specified how to containarize which is present in Dockerfile. Its structure will be explained shortly.

## Installation

It comes in two flavors in Windows, one as windows container and linux container (preference and recommended: Linux).Linux setup uses WSL2 as backend. So these windows features must be turned on Linux users already have their machine’s OS as backend. Installation guide can be followed from here: [Install Docker Engine | Docker Documentation](https://docs.docker.com/engine/install/). Will meet you after the installation cause parts below is going to be hands on.

## Dockerfile Structure

Before deep diving into the Docker World, first lets see what we are getting out of Docker containers. Lets create a Dockerfile first as below with the contents as:

```docker
FROM python:3.9.7-alpine

RUN pip install --upgrade pip

COPY ./requirements.txt .
RUN pip install -r requirements.txt

COPY ./sf23 /app
WORKDIR /app

RUN python manage.py migrate
```

Dont worry what the first line says (it comes later), the other lines of code must be clear. We specify the path where the image will be stored. Then it copies our project directory to that path, then different essential commands are run to install modules upon that same path. And finally `python [manage.py](http://manage.py) migrate` is a command to runserver in a container.

## Build and Run

Lets build and run to see what it does. Don’t worry the explanation will come.

Docker command: `docker build -t <image-name>` builds the docker image from the specification specified in Dockerfile. Image-name refers to the name of image, we can also specify tag as to indicate the version of image we are working on.

`docker run <image-name>` runs the instance of image. Different arguments like port no, file system, volumes etc can be included to create this instance. This instance is called a container.

So what are images and containers, what do each represent? Images are simply the specifications for the instance or container to run. In Dockerfile, all the lines of codes written are specifications of how an instance should run. When we perform `docker build`, what is does is simply package all the specifications (it may fetch base/parent images which we’ll come later). Containers however are the running instance of a image; that means the application is containarized with those specification (image) and different arguments can be specified to run it however we want.

## Parent Image

We discussed above that the lines of code in Dockerfile are specifications and in specific term each line of code is called a layer. Each layer is an image in itself. The bottom layer upon which other layers are built is called parent image. Typical parent image is host kernel on top of which our project specifications are written. It is required cause our project requires file system and commands to run like ls,cd,python etc. It provides limited userspace thats why its not a bull blown VM. Instead of virtualization of hardware, its sharing the machines’ (WSL2’s if you are using Linux engine in windows) resources. So therefore the containers’ parent image should be same as machines’ kernel.

## Compose

Imagine a scenario, where you want to run a one django service, one node service and also a database. From what we have learnt, we had to specify our environment based on the service we were to run in Dockerfile. Building images would be similar but running it we will have to manually run commands for each service manually.
`docker run [OPTIONS] -p port:port <image-name>`

Instead of doing this tedious job, we have a tool called compose that comes pre-installed with docker. It is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services. Then, with a single command, you create and start all the services from your configuration. `docker compose up` then builds and starts all the container services in the configuration.

## Compose YAML Structure

Compose file configuration is stored in docker-compose.yml file. YAML is similar structure to JSON (dont worry if you don’t know what this is) but with indentation structure. A typical way to write docker-compose.yml for our django application is shown below:

```yaml
version: "3.9"

services:
  web:
    volumes:
      - static:/static
    env_file:
      - .env
    build:
      context: .
    ports:
      - "8000:8001"
```

Different services that we use comes under services section with our container alias mentioned and specification within that particular service. Dont worry about all the code that you see here, we’ll slowly explain different parameters mentioned here.

## Port Mapping

Port mapping is used to access the services running inside a docker container. From our yml file above we see that `ports: - "8000:8001"`. It means it maps the host’s port 8000 to port 8001 inside that container. So we can access the application hosted in 8001 port using 8000 on the host machine. Other mapping are also similar as port mapping.

## Volumes

We also see volumes section in our yml file structure. It is the preferred method for persisting data. Since container is a instance running, any configurations that changes in that instance, once the container stops running; the data is lost. So volumes are used in the case.

- Volumes are stored in `\\wsl$\docker-desktop-data\data\docker\volumes` in windows’
- Volumes are stored in `/var/lib/docker/volumes` in linux

One thing that volumes are also used for is sharing data or communicating between different containers.

## Dockerizing Project

To dockerize our project we follow the following steps.

- First write our Dockerfile as below:

```docker
FROM python:3.9.7-alpine

RUN pip install --upgrade pip
COPY ./requirements.txt .
RUN pip install -r requirements.txt

COPY ./sf23 /app
WORKDIR /app

RUN python manage.py migrate --no-input && python manage.py collectstatic --no-input

CMD [ "python","manage.py", "runserver", "0.0.0.0:8000" ]
```


- We then write docker-compose.yml file to mention how different containers(one container for now but will come later) can run as below

```yaml
version: '3.9'

services:
  web:
    volumes:
      - static:/static
    build:
      context: .
    ports:
      - "8000:8000"

volumes:
  static:
```

- `.dockerignore` ignores the files that images dont require in the project. We’ll empty for now.
- Now we are ready to employ `docker compose build` to build the image.
- `docker compose up` to run the image.

## Adding Nginx

In the Nginx configuration mentioned in previous module, we listen on port 80 (http port) to recieve request from the clients, then the nginx server fetches us the service from the location route and send it back to client. Keeping this in mind, in our docker-compose.yml file in the project directory, we add the following service:

```yaml
version: "3.9"

services:
  web:
    volumes:
      - static:/static
    build:
      context: .
    ports:
      - "8000:8000"
  nginx:
    build: ./nginx
    volumes:
      - static:/var/www/static
    ports:
      - "80:80"
    depends_on:
      - web
volumes:
  static:
```

Note that we have used volumes section at the end there that suggest where all the containers look for during communication. Since we are listening on port 80, we need to map any other port we decide to give access to outside user to port 80 (or 443 for https) on the container, because thats where our service will be listening. Since we are building off of `./nginx` location we need to add a Dockerfile in our nginx folder as well.

```docker
FROM nginx:1.19.0-alpine

COPY ./default.conf /etc/nginx/conf.d/default.conf
```

The default.conf file has been described in our previous module. The same file is copied into nginx directory. Now we are again ready to docker-compose up. Lets try it. Wait a second it doesn’t work. Whats missing is that we are sending http request from the server but our django application doesn’t understand html requests, we need to use gunicorn command instead of runserver in Dockerfile

```Dockerfile
FROM python:3.11.0b4-alpine3.16

COPY ./requirements.txt /sf23/requirements.txt
RUN pip install --upgrade pip
 
WORKDIR /sf23
RUN pip install -r requirements.txt

COPY ./sf23 /sf23

RUN python manage.py migrate --no-input && python manage.py collectstatic --no-input
CMD [ "gunicorn","sf23.wsgi:application", "--bind", "0.0.0.0:8000" ]
```
Note that it still doesn't work if you try to build because now we are using HTTP port that should be allowed in our development environment in settings.py inside of your project directory and set allowed hosts like this:
`ALLOWED_HOSTS = ["*"]`
Now finally we can `docker compose build --no-cache` to fresh build without previous caches and then `docker compose up` to run the containers.

## Docker Hub

Docker Hub is a docker registry service that hosts and distributes docker images. It is similar to Github but for docker images only. To push your newly created images into docker hub we follow the following procedures:

- First create an account on Docker Hub
- From shell type in `docker login` to login into your docker hub account
- Create tag for your image so that you can push it as below:
  `docker tag <local-project-image> <user-name>/<image-name>:<tag>`
- Now push it to the docker hub using `docker push <user-name>/<image-name>:<tag>`

To pull the existing images into your local machine you do the above login procedure and type in:

- `docker pull <user-name>/<image-name>:<tag>`

> written by Aagat