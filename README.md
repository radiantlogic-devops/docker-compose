# Docker Compose

Docker Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services. Then, with a single command, you create and start all the services from your configuration. <br><br>
Compose works in all environments: production, staging, development, testing, as well as CI workflows. 

> A curated list of Docker Compose samples.

These samples provide a starting point for how to integrate different services using a Compose file and to manage their deployment with Docker Compose.

> **Note:**
>
> The following samples are intended for use in local development environments such as project setups, tinkering with software stacks, etc. These samples must not be deployed in production environments.

## Getting started

These instructions will get you through the bootstrap phase of creating and
deploying samples of containerized FID/Zookeeper deployments with Docker Compose.

### Prerequisites

- Make sure that you have Docker and Docker Compose installed
  - Windows or macOS:
    [Install Docker Desktop](https://www.docker.com/get-started)
  - Linux: [Install Docker](https://www.docker.com/get-started) and then
    [Docker Compose](https://github.com/docker/compose)
- Download some or all of the samples from this repository.

### Running a sample

The root directory of each sample contains the `docker-compose.yaml` which
describes the configuration of service components. All samples can be run in
a local environment by going into the root directory of each one and executing:

```console
docker-compose up -d
```

Check the `README.md` of each sample to get more details on the structure and
what is the expected output.
To stop and remove all containers of the sample application run:

```console
docker-compose down
```
