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