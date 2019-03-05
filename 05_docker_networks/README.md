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

## CLI Management

- `docker network ls` -> show networks
- `docker network inspect` -> inspect a network
- `docker network create <optional: --driver>` -> create a network
- `docker network connect` -> attach a network to container
- `docker network disconnect` -> dettach a network from a container
- `docker container run -d --name <container_name> --network <network_name> <image>` -> to start a new container with a specific network

There are 3 networks by default on docker:

- `bridge` network is the default virtual network all containers are attached to
- `host` its a special network that skips the docker virtual network and attach it to the host's network directly; this sacrifices security of the container model but it also might improve performances
- `none` removes `eth0` and only leaves you with `localhost` to interact with

## Default Security

- create your apps so FE/BE sit on the same Docker network
- their inter-communication never leaves host
- all externally exposed ports closed by default
- you **must** manually expose via `-p`, which is better default security
- this gets better with Swarm and Overlay networks