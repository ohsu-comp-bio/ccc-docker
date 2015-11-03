# CCC Docker Configuration #

This repository contains [Docker Compose](https://docs.docker.com/compose/)
configuration for managing a development environment for CCC Development. This
approach has a number of benefits, including:

  + Using a collection of services built using Phusion's
    [`baseimage`](phusion.github.io/baseimage-docker/). This allows use to
    properly maintain an init process, multiple processes per service, and
    logging.

  + An intuitive directory configuration. The contents of each directory in the
    project gets copied to the root of the container. Note how we use git
    submodules to deploy code in `/opt/xxxx` to the container.

  + We can use [nginx-proxy](https://github.com/jwilder/nginx-proxy) to provide
    intuitive access to services via subdomains. We assume that you have a
    [Pow](https://pow.cx) or Hosts file configuration for `ccc.dev`.
    Services can be set up such as:

      + http://galaxy.central-function.ccc.dev

      + http://labkey.portland.ccc.dev

    See the `docker-file.yml` for how we specify the subdomain via the
    `VIRTUAL_HOST` environment variable.

  + The use of [data
    containers](https://medium.com/@ramangupta/why-docker-data-containers-are-good-589b3c6c749e)
    to persist data between container instances. This ensures that you don't
    have to reinstall Python eggs, re-run migrations, etc.

## Avaiable Services ##

  + Galaxy at http://galaxy.central-function.ccc.dev

## Dependencies ##

Please make sure that you're able to properly run Docker Compose before
configuring this app.

Also, in order for `nginx-proxy` to communicate to the Docker daemon, you need
to have the following environmental variables set:

    + DOCKER_HOST
    + DOCKER_TLS_VERIFY
    + DOCKER_CERT_PATH

Note that these are already available if using Docker Machine when running
`eval $(docker-machine env ccc)`.

## How to install ##

1. Check out this repo.

2. Run `git submodule init && submodule update` to load appropriate submodules.

3. Run `docker-compose up`.
