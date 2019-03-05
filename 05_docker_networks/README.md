## Docker Networks Defaults

- each container connects to a private virtual network called `bridge`.
* each virtual network routes through NAT firewall on host IP.
  * docker deamon configures the host IP address on its default interface, so container can get out to the internet and back.
- all containers on a virtual network can talk to each other without `-p`.
* best practice is to create a new virtual network for each app
  * network `my_web_app` for `mysql` and `php/apache` containers
  * networl `my_api` for `mongo` and `nodejs` containers

All of this is configurable but works in most cases(specially for test/dev environments).

* Docker containers don't use the same IP as host by default
  * `docker container inspect --format '{{ .NetworkSettings.IPAddress }}' <container_name>` will show the actual IP address for the container
- `docker container port <container_name>` to print out the container's port its listening to 
