# standalone one node FID

Example docker-compose.yaml file for single-node(standalone) FID deployment with CFS

## Prerequisites
> check and install following if they are not available on the server
- Docker desktop for Windows v20.x or higher
- Hyper-v enabled
- Running Linux containers on Windows and platform support in Docker Compose requires Windows 1803 or greater.

> Run Docker for Windows in “mixed” mode by running Windows and Linux containers together
- Switch to Windows containers in Docker for Windows tray
- Go to Docker Engine settings section and set experimental parameter to ‘true’
- Apply and restart the docker
- Check `docker version` should show 
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
> Sample .env file
```
# Example .env file
FID_IMAGE=radiantone/fid
FID_VERSION=7.4.0-ea
CLUSTER_NAME=fid4cfs
FID_PASSWORD=Radiant1Rocks
LICENSE=PASTE_YOUR_LICENSE_HERE
```
> Clone this project locally or copy the files `docker-compose.yaml` and `.env` locally.

## Usage
- The following command will show you all the logs & will be useful to troubleshoot any issue while container is spinning up
```
docker-compose up 
```
- Use this following command to spin up the container in the background
```
docker-compose up -d
```
- To bring down and delete the container 
```
docker-compose down
```
> Note: Above command will not delete any volumes created while setting up container, Add `-v` flag to delete volumes as well `docker-compose down -v`

> Following usage command have been tested on docker version `20.10.8` & docker-compose version `1.29.2`

Once the container is up, Login into main control panel on port 7070 of the docker host `http://<DOCKER-HOST IP-ADDRESS OR HOST-NAME>:7070` and use `cn=Directory Manager` as username and `secret1234` as default password
