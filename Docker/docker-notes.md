# Docker 

## What is it?

Service that runs/manages containers.

## Containers

A container is an isolated software environment. The idea is that it allows people with different computers (e.g. Mac vs windows, windows 8 vs windows 10 etc.) or different versions of programs (e.g. nvm 12 vs nvm 16) to be able to run the same application. 

Containers run code. If the code that the container is instructed to run comes to and end, it will exit the process. However, if the container is something like a server, it may just keep running until it receives a terminal command to exit. 

## Image

A description of how to build a container. This contains all the instructions of how to create a container for the application to run.

## Analogy

Containers are like a box. Images are like instructions on how to make a box. 

One image could be: made out of cardboard, cube shape, red wrapping paper and gold bow.
Second image could be: made out of wood, triangular prism shape, green wrapping paper and no bow. 

Both are boxes but instructions on how to make the box differ significantly. In the same way every container has the same purpose but each one can be unique depending on the instructions (code) contained in the image.


##Running Containers

docker ps => list containers (default: only running containers).
docker ps -a => list every container - including inactive ones.
docker ps -q => (-q = quietly) lists every container (including inactive) but only the ID column.
docker ps -aq => lists every container (even inactive) by only their ID column.

docker run <image-name> => start a new container based on an image.
docker rm <container-name> => delete an inactive container.
docker pull <image-name> => If this image is not on your computer, this is the command to run to bring the image onto your computer. Bear in mind, however, that you can simply do “docker run … “ since if the image is not on your computer, it automatically runs “docker pull … “.

Other docker commands

Docker image —help. => Using —help flag, generally, is quite useful in docker.
Docker images => lists all docker images on your computer.
Docker image ls => lists all docker images on your computer.
docker rmi <image_id> => Removes a docker image. NOTE: in order to delete an image, you must first delete the container(s) associated with the image.
docker system prune => Remove all docker containers
Docker system prune —volumes —remove-orphans
docker system prune -a => remove all Docker items
docker rm $(docker ps -aq) 
echo "docker rm $(docker ps -aq)" > ./utility-scripts/cleanup.sh.  => Allows you to store a terminal command in a bash script file and automatically creates the new file cleanup.sh (assumes you’ve already made a directory called utility-scripts).
nano ./utility-scripts/cleanup.sh => allows you to open a file in the terminal and edit it. => To run a bash script (.sh file), start the terminal command by typing ‘bash’ followed by file name (bit like ‘node index.js’). 

NOTE: it may be the case that nano does not work. If that’s the case, try cat instead:

cat ./utility-scripts/cleanup.sh


## Docker Hub

Docker hub is essentially like a registry you can go to to look at and store docker images.


## Docker Containers (more)

You can do:
.
docker run -it <image-name> => the -it flag lets docker know you want to create an interactive terminal.
exit() => This allows you to exit the interactive terminal and the container (assuming your using python)
process.exit() => allows you to exit interactive terminal which uses node.

docker run -it [image name] [optional command]
e.g. docker run -it python bash => That would open a bash terminal
exit => all you need to type to exit a bash terminal.

docker start -i [containerID] => Allows you to go back into pre-existing containers and see any files you have created in that container. 
Docker stop [containerID] => Stops a running container.

docker image rm $(docker image ls -q)
docker rmi $(docker images -q) => alternative way to remove all docker images. Note: first remove all containers before doing this.


## Bind Mounts

Allows you to pinpoint folders/files inside a container and store them on your local machine. Allows you to hook a folder on the container up to a folder on the host machine.

—mount type=bind,src=[host folder], dst=[container folder] ==> essentially creates a permanent connection which binds a folder on your local machine (src) to a destination folder inside your container (dst). 

Assume you’re in a directory where inside is a folder called ‘python-folder’. 

An example of a terminal command which would bind a mount would be:docker run -it —mount type=bind,src=$(“pwd”)/python-folder,dst=/code python bash

docker run -it —mount type=bind,src=$(“pwd”)/python-folder,dst=/code -w /code python bash => the -w /code starts the new terminal in the code folder - not the root folder.

Note creating a bind mount in this way creates a two-way system. Not only can files created inside the code folder in the machine be sent to the python-folder, files created in the python-folder will then simultaneously be created in the code folder in the container.

When setting up an application, make sure you’re installing all relevant files and packages from the terminal that’s inside docker container. For example, running npm I should be done in the container terminal because it will install packages in a way that relevant to the version of node being used in that container.


docker run -it —mount type=bind,src=$(“pwd”)/node-folder,dst=/code -w /code -p 3000:3000 node bash => the -p flag allows you to connect a specific port inside your container to a port on your local machine. This means that if you were to run an express server from inside a container, you could go to google chrome on your local machine, go to localhost 3000 and your server would be available.

### -e

The e flag is important for feeding in info and values for variables. 

NOTE: for every variable you wish to input, you must have a corresponding -e. For example, imagine you had two variables - PORT and apiKey. Your docker command would include “… -e PORT=3000 -e apiKey=dskjcbkewjdckw…”. 

### -c 

The c flag is used to instruct docker to run certain commands as soon as the container starts running. 

Typical format is: -c [command]

For example:

Docker run -it —mount type=bind,src=$(“pwd”)/node-folder,dst=/code -w /code -e PORT=3000 -p 3000:3000 node bash -c “npm run dev” 

Or: 

Docker run -it —mount type=bind,src=$(“pwd”)/node-folder,dst=/code  -e PORT=3000 -p 3000:3000 node bash -c “cd code && npm run dev”

-d

The d flag is used to run a container in the background in detached mode. A good example of something to run in the background is a database. 

Docker run -d -e POSTGRES_PASSWORD=password -e POSTGRES_DB=rollercoasters -e POSTGRES_USER=admin postgres  

Docker exec -it [container-name/id] bash.

If running a postgres db, you can use psql in the terminal to interact with it. 

Docker exec [containerID] [command] - runs a command in a running container. Docker exec is NOT appropriate for a container that is inactive/ doesn’t exist.


-v (Volume flag)

Volumes allow for data inside the container to persist after the container has stopped running. 

An example of part of a docker command may be:

-v pgData:/var/lib/postgresql/data     => The bit after the colon is essentially an absolute path that begins from the root of the docker machine. pgData is a volume that is generated and is attached to the container. You would find a volume named pgData in the volumes section of the Docker GUI. 


YAML

Docker commands are obviously very long and precise. Moreover, to run a full application it may be the case that you need to run multiple containers simultaneously (E.g. container for a front end, container for a back end, container for a database) and have them connected and talking to one another. A good way to do this is to put all your docker commands in a yaml file, which you can simply run and it does it all for you.

Features of a YAML file

1. Services - services are just docker containers. 
2. Image - This is just the docker image you want to help create the container. 
3. Ports - potentially you will want to run a container on a port - both on local machine and container.
4. Environments - these are just variables you may need to feed in for the container to run.
5. Volumes - these are specified if you wish to persist data even after the container becomes inactive.
6. Network(s) - these are links which connect different containers together and allow them to pass data to each other.
7. Version - this goes at the top of a yaml file. It’s usual to choose version 3.


Example of a YAML file

Imagine you had a docker command that looks like this:
Docker run -it —mount type=bind,src=$(“pwd”)/node-folder,dst=/code -w /code -e PORT=3000 -p 3000:3000 -v pgData:/var/lib/postgresql/data node bash -c “npm run dev” 

Note: for the -p flag, the first number is for the port on your local machine, the second number is for the port inside your docker container. In short, imagine you had node server which ran on port 5000 inside your docker container. If your docker command had “-p 3000:5000” this would mean your server would be accessible on google chrome on your local machine if you went to localhost 3000. 

This could be translated into a YAML file that looks like this:

services:
    api:
         image: node
         volumes: 
                 - type: bind
                  - source: ./node-folder
                 - target: /code
         ports: 
                   - 3000:3000
         environment:
              - PORT=3000
         working_dir: /code
         command: bash -c “npm run dev”
     db:
         image: postgres
         volumes: 
             - type: bind
             - source: ./postgres-folder
             - target: /docker-entrypoint-initdb.d
          environment:
             - POSTGRES_PASSWORD=password
             -  POSTGRES_DB=rollercoasters
             - POSTGRES_USER=admin
             - pgData:/var/lib/postgresql/data
volumes: 
    pgData:
  

— end of yaml file —

Note: it may look like the file is incomplete due to that pgData key right at the bottom with nothing after it. It is NOT incomplete - the way It is written is sufficient. 

Note: sometimes there are hyphens used. To understand the significance of the hyphens, first understand that everything with a colon after is like a key in a json object. If it’s just a single value (e.g. the key of type simply has a value of “bind”) then that becomes a string. If there are multiple values, however, the hyphens signal that a particular key has an ARRAY of values. The hyphen indicates that something is another value in the array. Bear in mind, the arrays are arrays of objects.

 
You could then run that YAML file from the same directory that the yaml file is located by running the command:

docker compose up

Docker compose down => takes everything back down

Bear in mind, if you use the docker compose up command, it is looking for a file named docker-compose.yaml . If your file name is not called docker-compose, you can use the -f flag to point Docker to the file you want to use to spin up your containers. For example:

Docker compose up  -f go-bananas.yaml 


Other Miscellaneous Docker Stuff

Docker inspect [containerID] => allows you to get some general info about the state of the container.

Container Tags

Say you run the command “docker run postgres”. This assumes in effect you are running “docker run Postgres:latest”.

Tags allow you to specify the version of an image you wish to use to create a container.

<image-name>:<image-version>


Create own Docker image using Dockerfile

Questions to be answered (in this order) when creating own Docker image:
1. What operating system are you using?
2. Does operating system need to be updated for Docker engine to work on it ?
3. What dependencies does your application have? Python/Node etc.?
4. How to install these dependencies on your new OS?
5. How to get the source code of your app into the container?
6. Commands that need to be executed in order for your app to run when the container becomes active? 
Example of a Dockerfile:

—start of docker file—-

FROM Ubuntu

RUN apt-get update                                      
RUN apt-get install python                            // Note: RUN apt-get is specific to the ubuntu OS.

RUN pip install flask
RUN pip install flask-mysql

COPY . /opt/source-code

ENTRYPOINT FLASK_APP=/opt/source-code/app.py flask run


— End of docker file —

Once you’ve created your docker file you can build it by running the command (in the same directory as where the docker file is):

Docker build  . -t <name-of-image>    => that full stop should be included


NOTE: bear in mind, if you want to inspect the contents of a file in the terminal, you can use the nano command. Example:

nano Dockerfile



Entrypoint

Entrypoint provides a way to have a dynamic docker command for your custom built image.

Imagine your Dockerfile included this:

ENTRYPOINT[“sleep”]

You could then specify a docker command like this:

Docker run <image-name> 10 

What this would do is cause the machine to read the command sleep and execute that command sleep for 10 seconds.

If you then ran:

Docker run <image-name> 600

It would sleep for 10 minutes.

If you have an ENTRYPOINT, it is also wise to have a CMD to serve as a default parameter value for your entrypoint command.

You could have:

ENTRYPOINT[“sleep”]

CMD[“5”]


Note: you can override the ENTRYPOINT that has been described in the docker file by using the —entrypoint flag in your docker command. 

For example,

docker run —entrypoint sleep2.0 ubuntu 

docker run -d --entrypoint sleep ubuntu 1000 => This issues the command of sleep for 1000 seconds.

This would override the ENTRYPOINT[“sleep”]


Note: final and complete command run once container is spun up will be a combo of ENTRYPOINT + CMD. 


—name 

The —name flag can be used to name containers. 

For example:


Docker run —name hello-world node 

The image is node but name of container is hello-world.


Connecting docker containers (so they can communicate with one another) => —link & network

The —link flag is used to connect different docker containers. In a YAML file, you would use the links key to connect containers together. Links uses a hyphen for each link in the yaml file since the links key has an array value.

Example:

docker run --name clickcounter --link redis:redis -p 8085:5000 kodekloud/click-counter 

Note: —link was the old-fashioned way to do it.


Networks

When you first install Docker, it creates 3 networks automatically: Bridge, none and host.

To see all the Docker networks available on your computer, you can run:

docker network ls

To see the IP address for a Docker network, simply use:

docker inspect [networkID]
