# **Docker**
- platform to build, run and ship application in a consistent way
- application may not be functioning on other machines due to: **Files Missing, Software version mismatch, different configuration settings (environment variables)**

# **Docker Architecture**
- uses **client-server architecture**, has a client component that talks to server component (docker engine) using a RESTFUL API
- technically Docker is just like a normal process running on a computer (shares the kernel of the host, kernel manages application and resources)

# **Conatiner VS Virtual Machines**
## **1. Containers**
- isolated environment for running an application
- lightweight
- shared the same OS as the host
- start quickly
- requires less hardware resource
## **2. Virtual Machines**
- abstraction of machine (physical hardware)
- can several virtual machines of a real physical machines, eg: using hypervisor to run windows and LINUX on a **MAC** machine, hypervisor is a tool to create and manange virtual machines
### **Cons:**
- each VM needs a full-blown OS (needs to be licensed, patched and monitored)
- slow to start (entire OS has to be loaded)
- resource intensive (each VM takes a slice of the actual physical hardware resources)
- usually have a limit on the number of VM we can run on a machine

# **Development Workflow**
- dockerize the app that we want to deploy (by adding a docker file that packages the app into an image)
- docker image generated contains everything that the application needs to run (cut-down OS, runtime env, app files, 3rd party libraries, env variables)
- spins up a container (it's just a process) by loading the corresponding image
- image has file system
- need to give image a tag for versioning & identification purpose
```docker
# Dockerfile

FROM node:alpine
COPY . /app
# copy all the files in the current directory into the app dir

WORKDIR /app
# set the current working dir to /app

CMD node app.js
# run the command "node app.js" inside the container when deployed
```
## **Docker basic commands**
### **1. Building a Docker Image**
```cmd
docker build -t hello-docker .
// build an image with hello-docker as the tag name
// find the relevant Dockerfile in the current directory
```
### **2. Check all the docker images**
```cmd
docker image ls OR docker images
```
### **3. Run a docker image**
```cmd
docker run <image-name>
```
### **4. Push a docker image to docker hub**
```cmd
docker tag <image-name> <username>/<docker-repo-name>:<docker-tag-name>
// docker tag "name of the image" "docker username"/"docker repo name":"docker tag name"
docker push <username>/<docker-repo-name>:<docker-tag-name>
// docker push "docker username"/"docker repo name":"docker tag name"
```
### **5. Pulling a docker image from docker hub**
```cmd
docker pull <username>/<docker-repo-name>
```
### **6. Removing docker containers or images**
```cmd
docker rm <container_id> // removed a stopped container
docker rm -f // force the removal of a running container
docker rmi <image_id>
docker rmi -f <image_id>
```
### **7. Others**
```cmd
1. docker ps == docker container ls// get all the container process running in docker
2. docker ps -a // list all the stopped containers
3. docker run -it <image_name> // start a container process in interactive mode
4. docker ls -q // return the image ID of all the docker images
5. docker image rm $(docker ls -q)
6. docker inspect <container-id>: inspect the details of the container
```

# **Linux in Docker**
- Linux has an package manager called **apt** (stands for advanced package tool)
- **nano** is a basic text editor in linux
- linux has a package database that contains hundreds of packages
- linux file system is organized if tree structure (hierarchical structure)
- everything in linux is a folder (blue files represent a directory)
## **Basic Linux commands:**
1. echo $0: get the location of the shell program
2. history: get all the command executed lately
3. apt list: get all the package installed
4. apt update: update the package database
5. ls: list all the files and folders in current working directory
6. pwd: print working directory
7. cd ~: go to the **HOME** dir
8. mv test docker: rename the file name from test to docker OR to move files
9. rm filename: remove the file called "filename"
10. rm -r file/: remove all the files in the "file" folder recursively and finally remove the folder
11. touch filename: create a new file called "filename"
## **Commands to deal with file**
1. nano docker: edit the file named "docker"
2. cat docker: see the content of the file named "docker"
3. more docker: read the file named "docker"
4. less docker: read the file named "docker"
5. head -n 5 docker: only get the first 5 lines of the file named "docker"
6. tail -n 5 docker: only get the last 5 lines of the file named "docker"
## **Redirection in Linux**
1. cat file1.txt file2.txt > file3.txt: concatenate all the contents in file1.txt & file2.txt and move it to file3.txt
