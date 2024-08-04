# edgefoundrydevcontainer
DEM DevContainer Egde Foundry

This repository contains the docker compose files for EdgeX releases. 

> **Note:** Each release is now on it's own branch named after the release codename. You can view all branches [here](https://github.com/edgexfoundry/edgex-compose/branches/all).

This `branch` contains the `pre-release` docker compose files that pull and run the EdgeX images from the Nexus3 docker registry that are tagged with `master`. These images are built from the Edgex CI Pipeline when PRs are merged into the `master` branch.

> **Note**: Docker does not re-pull newer instances of these images. You must pull the new image instances. See the `make pull` command described below that will do this for you.

These `pre-release` docker compose files are generated from the multiple source compose files located in the `compose-builder` folder. See [README](compose-builder/README.md) there for details on regenerating these files after making changes to the source files.

### Compose Tool

The Makefile in this folder expects the `docker compose` CLI command.
The old stand-alone `docker-compose` tool is no longer supported.
See https://docs.docker.com/compose/install/ for installation details for the latest `docker compose` CLI command.

### Compose Files

This folder contains the following compose files:

#### Generated Compose files

> **NOTES: **
>
> - *DO NOT EDIT the files directly for permanent changes. Make all permanent changes to the source compose files in the `compose-builder` folder and then regenerate these files*
> - Use `make build` from `Compose Builder` to regenerate all the following compose files.
> - See each description for the convenience `make` commands that are provided to work with each of these compose files.

- **docker-compose.yml**
    Contains all the services required to run in secure configuration. Includes the Device Virtual & Device REST device services and the UI.
    **Make Commands** 
    
     - Use `make run <service(s)>` and `make down` to start and stop the services using this compose file.
    
     - Use `make pull <service(s)>` to pull all or some images for the services in this compose file.
    
     - Use `make get-token` to generate a Kong access token for remote access of the services running from this compose file.
    
- **docker-compose-arm64.yml**
    Contains all the services required to run in secure configuration on `ARM64` system.  Includes the Device Virtual & Device REST device services and the UI.
    **Make Commands** 
    
     - Use `make run arm64` and `make down` to start and stop the services using this compose file.
     - Use `make pull arm64 <service(s)>` to pull all or some images for the services in this compose file.
     - Use `make get-token arm64` to generate a Kong access token for remote access of the services running from this compose file.
    
- **docker-compose-with-app-sample.yml**
    Contains all the services required to run in secure configuration with Sample application service.  Includes the Device Virtual, Device REST, UI & App Sample services. Use this version when using the UI to make changes to the configurable pipeline on the Sample application service.
    **Make Commands**

    - Use `make run app-sample` and `make down` to start and stop the services using this compose file.
    - Use `make pull app-sample <service(s)>` to pull all or some images for the services in this compose file.
    
- **docker-compose-with-app-sample-arm64.yml**
    Contains all the services required to run in secure configuration with the Sample application service on `ARM64` system .  Includes the Device Virtual, Device REST, UI & App Sample services. Use this version when using the UI to make changes to the configurable pipeline on the Sample application service.

    **Make Commands**

    - Use `make run no-secty app-sample arm64` and `make down` to start and stop the services using this compose file.
    - Use `make pull no-secty ui app-sample <service(s)>` to pull all or some images for the services in this compose file.

- **docker-compose-no-secty.yml**
    Contains just the services needed to run in non-secure configuration.  Includes the Device Virtual & Device REST device services and the UI.
    **Make Commands**

    - Use `make run no-secty` and `make down` to start and stop the services using this compose file.
    - Use `make pull no-secty <service(s)>` to pull all or some images for the services in this compose file.
    
- **docker-compose-no-secty-arm64.yml**
    Contains just the services needed to run in non-secure configuration on `ARM64` system.  Includes the Device Virtual & Device REST device services and the UI.

    **Make Commands**

    - Use `make run no-secty arm64` and `make down` to start and stop the services using this compose file.
    - Use `make pull no-secty arm64 <service(s)>` to pull all or some images for the services in this compose file.


- **docker-compose-no-secty-with-app-sample.yml**
  Contains just the services needed to run in non-secure configuration with Sample application service.  Includes the Device Virtual, Device REST, UI & App Sample services. Use this version when using the UI to make changes to the configurable pipeline on the Sample application service.
  **Make Commands**

  - Use `make run no-secty app-sample` and `make down` to start and stop the services using this compose file.
  - Use `make pull no-secty app-sample <service(s)>` to pull all or some images for the services in this compose file.

- **docker-compose-no-secty-with-app-sample-arm64.yml**
  Contains just the services needed to run in non-secure configuration with the Sample application service on `ARM64` system .  Includes the Device Virtual, Device REST, UI & App Sample services. Use this version when using the UI to make changes to the configurable pipeline on the Sample application service.

  **Make Commands**

  - Use `make run no-secty app-sample arm64` and `make down` to start and stop the services using this compose file.
  - Use `make pull no-secty app-sample <service(s)>` to pull all or some images for the services in this compose file.

- **docker-compose-openziti.yml**
  Contains the services needed to bring OpenZiti online, configure it, and enable consul to perform underlay-based health checking. Used in conjunction with `make run (pull) zero-trust`. This compose file should be started before starting the `make run zero-trust` compose file.

  **Make Commands**

    - Use `make openziti` and `make openziti-down` to start and stop the services using this compose file.
    - Use `make openziti-clean` to remove all stopped containers, all volumes and all networks used by the EdgeX stack. Use this command when needing to do a fresh restart. **Note** You must _also_ run the corresponding `make down zero-trust` command to fully clean up.
    - Use `make openziti-logs` to follow the logs
  
### Additional make commands

- `make clean`

    Runs `down` command and removes all stopped containers, all volumes and all networks used by the EdgeX stack. Use this command when needing to do a fresh restart.
    
- `make get-token`
    For secure mode only. Runs commands via docker to generate a new API Gateway token.

- `make get-consul-acl-token`
  For secure mode only. Runs commands via docker to retrieve a Consul Access token.

### Additional compose files

- **docker-compose-portainer.yml**
    Stand-alone compose file for running Portainer which is a  Docker container management tool. Visit here https://www.portainer.io/ for more details on Portianer.
    Use `make portainer`and `make portainer-down` to start and stop Portainer.