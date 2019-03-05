## Commands seen

* `docker container run -it` -> to start a new container interactively
  * this will start a new container
  * `-t` is for allowing a pseudo-tty(terminal)
  * `-i` keeps `stdin` open to receive more commands
  * example: `docker container run -it --name proxy nginx <command>`
* `docker container start -ai` -> to rerun a container that stopped
  * `-a` attaches `stderr` and `stdout` again to the container
* `docker container exec -it <container_name> <additional_command>` -> run additional commands in existing container
  * this will only work on an existing container
  * when exiting the terminal, the container keeps running since `exec` only attaches another command but won't affect the root command

### Alpine Linux

- very small linux distro (~5MB)
- focused on security