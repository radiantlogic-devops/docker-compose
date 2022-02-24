# FID deployment with CFS

Sample docker-compose.yaml file for single-node(standalone) FID deployment with CFS

## Prerequisites
> Check and install following if they are not available on the host
- This deployment is supported only on Windows physical hosts
- Running Linux containers on Windows and platform support in Docker Compose requires Windows 1803 or greater.
- Docker desktop for Windows v20.x or higher - https://www.docker.com/products/docker-desktop
- Hyper-v enabled - `Enable-WindowsOptionalFeature -Online -FeatureName $("Microsoft-Hyper-V", "Containers") -All`

> Run Docker for Windows in “mixed” mode by running Windows and Linux containers together
- Switch to Windows containers in Docker for Windows tray
- Go to Docker Engine settings section and set experimental parameter to ‘true’
- Apply and restart the docker
- Run `docker version` should show 
```
Client:
 Cloud integration: v1.0.22
 Version:           20.10.12
 API version:       1.41
 Go version:        go1.16.12
 Git commit:        e91ed57
 Built:             Mon Dec 13 11:44:07 2021
 OS/Arch:           windows/amd64
 Context:           default
 Experimental:      true

Server: Docker Desktop 4.5.1 (74721)
 Engine:
  Version:          20.10.12
  API version:      1.41 (minimum version 1.24)
  Go version:       go1.16.12
  Git commit:       459d0df
  Built:            Mon Dec 13 11:42:13 2021
  OS/Arch:          windows/amd64
  Experimental:     true
```

## Usage
> Clone this project locally or copy the files `docker-compose.yaml` and `.env` locally.

> Sample .env file
```
# Example .env file
FID_IMAGE=radiantone/fid
FID_VERSION=7.4.0-ea
CLUSTER_NAME=fid4cfs
FID_PASSWORD=Radiant1Rocks
LICENSE=PASTE_YOUR_LICENSE_HERE
```
### Start
- The docker-compose up command aggregates the output of each container. When the command exits, all containers are stopped. 
```
docker-compose up 
```
- Running docker-compose up --detach starts the containers in the background and leaves them running.
```
docker-compose up -d
```
### Stop
- Stop containers and removes containers, networks, volumes, and images created by up
```
docker-compose down
```
> Note: Above command will not delete any volumes created while setting up container, Add `-v` flag to delete volumes as well `docker-compose down -v`
### Status
- Lists all containers and their status
```
docker-compose ps
```

> Following usage command have been tested on docker version `20.10.8` & docker-compose version `1.29.2`

> Once the containers are up
- Login into main control panel on port 7070 of the docker host `https://<DOCKER-HOST IP-ADDRESS OR HOST-NAME>:7171` or https://localhost:7171
- Login to setup CFS https://localhost:8443/system and use the directory manager credentials

### Troubleshooting

> If docker deamon is not starting in windows container mode, Make sure Hyper-V & Continers feaure is enabled on the server/desktop

```
Enable-WindowsOptionalFeature -Online -FeatureName $("Microsoft-Hyper-V", "Containers") -All
```
Run the above command as administrator in prowershell and restart


> This following error is thrown when any of your host ports are been used by other services on the server/desktop

```
Error response from daemon: failed to create endpoint 09-cfs-fid-0-1 on network 09-cfs_fid-net: failed during hnsCallRawResponse: hnsCall failed in 
Win32: The process cannot access the file because it is being used by another process. (0x20)
```
You can troubleshoot this issue by using `netstat` to find `PID` of the process and take necessary actions
