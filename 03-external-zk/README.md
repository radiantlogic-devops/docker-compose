# 3node-external-zk


Example docker-compose.yaml file for three-node zookeeper deployment

## Prerequisites
> check and install following if they are not available on the server
- docker  [Download Instructions]: <https://docs.docker.com/get-docker>
- docker-compose [Download Instructions]: <https://docs.docker.com/compose/install>
- Create a bridge network with following name `zk-net` `docker network create --driver=bridge zk-net` (If you are changing the name from zk-net, Please update yaml files accrodingly)
- Prepare .env file for setting up the container or use sample .env file present in this directory
```
# Example .env file
ZK_VERSION=3.5.8
```
- Place `docker-compose.yaml` & `.env` file in directory and open terminal session

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

Once the containers are up, Check on port 18080 of the docker host `http://<DOCKER-HOST IP-ADDRESS OR HOST-NAME>:18080/commands/is_read_only` to see zookeeper ensemble is in read-write mode

Here is example output
```
{
  "read_only" : false,
  "command" : "is_read_only",
  "error" : null
}
```