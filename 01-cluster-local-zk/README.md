# 3node-fid-cluster-local-zk

Example docker-compose.yaml file for 3 node-cluster FID deployment

## Prerequisites
> check and install following if they are not available on the server
- docker  [Download Instructions]: <https://docs.docker.com/get-docker>
- docker-compose [Download Instructions]: <https://docs.docker.com/compose/install>
- Prepare .env file for setting up the container
```
# Example .env file
FID_VERSION=7.3.16
CLUSTER_NAME=3fid
ZK_PASSWORD=secret1234
LICENSE=PASTE_YOUR_LICENSE_HERE
```
- Place `docker-compose.yaml` & `.env` file in directory and open terminal session

## Usage
- This following command will show you all the logs & will be useful to troubleshoot any issue while constainer is spinning up
```
docker-compose up 
```
- Use this following command to spin up the continer in the background
```
docker-compose up -d
```
- To bring down and delete the container 
```
docker-compose down
```
> Note: Above command will not delete any volumes created while setting up container

> Following usage command have been tested on docker version `20.10.8` & docker-compose version `1.29.2`

Once the container is up, Login into main control panel on port 7070 of the docker host `http://<DOCKER-HOST IP-ADDRESS OR HOST-NAME>:17070` and use `cn=Directory Manager` as username and `secret1234` as default password