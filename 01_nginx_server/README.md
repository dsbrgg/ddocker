- **Image** is the application we want to run
- A **Container** is an instance of that image running as a process
- You can have many containers running off the same image

-------------------------------------------------------

Command in this lecture:

- `docker container run --publish 80:80 nginx`

What does this do?

- Downloads latest image `nginx` from Docker Hub
- Starts a new container from that image
* Opened port 80 on the host IP
	* Host port(left number) might give a "bind error" if already in use
- Routes the traffic to the container IP, port 80

In order to make it run in the background(without "freezing" the terminal):

- `docker container run --publish --detach 80:80 nginx`

Naming the container:

- `docker container run --name <name> --detach --publish 80:80 nginx`

Listing containers:

- old: `docker ps`
- new: `docker container ls`
- lists all containers: `docker container ls -a`

Stopping containers:

- `docker container stop <container_id>`

Checking logs from container:

- `docker container logs <container_name>`

Checking processes on container:

- `docker container top <container_name>`

Removing containers(if running, you gotta stop it first):

- `docker container rm <container_ids || container_names>`