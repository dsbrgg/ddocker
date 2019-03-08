# Docker Images

- `docker image ls` to check your installed images
- an image is the app binaries and dependencies and the metadata about the image and how to run the image
- not a complete OS
- the kernel comes from the host
* it can be really small
	* golang can export a single binary with all depedencies in it for a really small runtime
	* it can be a complete OS with a lot of things that will consume GB's of memory

## Docker Hub

- the "apt package manager" for Docker
- on production, one of the best practices is to never user the tag `latest` for your images
- specify a version and let another DevOps tool control versioning
- `latest` tags usually use heavier OS setup wether if you choose `alpine`, it will always be a lighter/compressed version of the image

## Image Layers

* `docker image history ls`
	* show layers of changes in the image
	* every image starts with a blank(scratch) layer
	* every set of changes on the filesystem in the image is a new layer

* `docker image inspect <image>`
	* shows details from the image binary/dependencies

- image layers are never duplicated, they are matched against a sha256
- if layer already exists, its just reused
- copying different source code ends up creating different images

* container layer based on image
	* docker creates a new read/write layer on top of that image
	* running two containers at the same time from the same image, would show only the difference between them
	* base image is *readonly*
	* when running containers and changing files from image in one running container, this is known as `copy on write(CoW)`
		* this will make the filesystem take that file out of the image and copy it into this difference(new container) and store a copy of that file in the container layer

## Image Tags

- `docker image tag <image_name[:tag]> <target_repo[:tag]>`
* `docker login` in order to be able to `docker image push` to your docker hub account
	* login info will be stored in `.docker/config.json`
	* `docker logout` in order to remove auth from the config file

## Dockerfile basics

* `docker build` will build from the default name for dockerfiles (eg. `Dockerfile`)
	* `docker build -f <dockerfile_name>` to use a dockerfile with a different name

* `FROM` command is required
	* package managers are usually one of the reasons to build contaienrs from an OS
	* you can use `FROM scratch` to start an empty container

* `ENV` are used to set environment variables

* `RUN` command to run shell commands/scripts
	* usually `RUN` commands will be run with chained commands in order to reduce the amount of layers created on the container

* `EXPOSE` command to open ports for the container in the virtual network

* `CMD` is required 
	* will run the actual software for the image with its possible configs