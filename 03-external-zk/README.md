# 3node-external-zk


Example docker-compose.yaml file for single-node(standalone) FID deployment

## Prerequisites
> check and install following if they are not available on the server
- docker  [Download Instructions]: <https://docs.docker.com/get-docker>
- docker-compose [Download Instructions]: <https://docs.docker.com/compose/install>
- Create a bridge network with following name zk-net `docker network create --driver=bridge zk-net` (If you are chnaging the name from zk-net, Please update yaml files accrodingly)
- Prepare .env file for setting up the container
```
# Example .env file
ZK_VERSION=3.5.8
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

Once the containers are up check on port 18080 of the docker host `http://<DOCKER-HOST IP-ADDRESS OR HOST-NAME>:18080/commands/is_read_only` to see zookeeper ensemble is in read-write mode

Here is example output
```
{
  "read_only" : false,
  "command" : "is_read_only",
  "error" : null
}
```