# CS 300: podman development environment

This is the CS300 development environment using podman instead of docker

Using podman for the department machines is necessary as it provides a rootless
environment and is almost a 1-to-1 replacement for docker.


## Building
Most of the structural changes happened within the Dockerfiles.

The Dockerfiles now do not create their own user - instead to ensure a seamless
connection with the CS filesystem we map the user's CS credentials into the container.

Therefore the Brown CS user `amiles6` will appear as that inside the podman 
container whilst having root privileges inside it.

The build script was changed to use podman and pass in a build argument

## Running

Their were only two changes to the run script:

1. `s/docker/podman/g` (replaced everywhere the word docker was with podman)
2. When starting a new container, the arg `--userns=keep-id` was added so the user
keeps their CS user id


## Getting started

```
# 1. build podman image locally
cd podman
./cs300-build-podman

# 2. start development environment
cd ..
./cs300-run-podman
```

## Potential Issues

I had one issue when trying to initially build - podman told me to try executing `podman system migrate` which fixed the issue so users may need to do this on department machines when using podman for the first time
