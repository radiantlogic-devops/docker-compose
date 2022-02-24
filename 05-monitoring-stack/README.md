# monitoring stack for FID

This example illustrates how to use Cloud Native Computing Foundation (CNCF) monitoring tools with a Radiantone FID stack.

The following table lists the actions you might want to take and the available tools.

| Purpose | Tool |
| --- | --- |
| **Monitor** | <ul><li>Radiantone FID</li></ul> |
| **Collect Metrics** | <ul><li>[Prometheus](https://prometheus.io/)</li><li>[Pushgateway](https://github.com/prometheus/pushgateway)</li><li>[FID-exporter](https://github.com/radiantlogic-devops/fid-exporter)</li><li>[Alertsmanager](https://github.com/prometheus/alertmanager)</li><li>[cAdvisor](https://github.com/google/cadvisor)</li></ul> |
| **Display Metrics** | <ul><li>[Grafana](https://grafana.com/)</li></ul> |
| **Generate Load** | <ul><li>pingidentity/ldap-sdk-tools</li></ul> |

By using this stack you can deploy FID cluster and monitor metrics in grafana generated whilst generating some traffic with searchrate,authrate & modrate

## Prerequisites
> check and install the following if they are not available on the server
- docker  [Download Instructions]: <https://docs.docker.com/get-docker>
- docker-compose [Download Instructions]: <https://docs.docker.com/compose/install>
- Prepare .env file for setting up the container or use sample .env file present in this directory
- Check your deployment server has enough memory for three node fid cluster and other services in this stack else you can comment fid-1, fid-2, fid-exporter-1 & fid-exporter-2 services in `docker-compose.yaml`
```
# Example .env file
FID_VERSION=7.3.16
CLUSTER_NAME=monitoring-fid
ZK_PASSWORD=secret1234
LICENSE=PASTE_YOUR_LICENSE_HERE
```

## Usage
- The following command will show you all the logs & will be useful to troubleshoot any issue while containers are spinning up
```
docker-compose up 
```
- Use this following command to spin up the container in the background
```
docker-compose up -d
```

Once the container is up, Login into main control panel on port 7070 of the docker host `http://<DOCKER-HOST IP-ADDRESS OR HOST-NAME>:7070` and use `cn=Directory Manager` as username and `secret1234` as default password 

To monitor metrics in grafana open port http 3000 of the docker host `http://<DOCKER-HOST IP-ADDRESS OR HOST-NAME>:3000` in browser and enter `username: admin` & `password: secret1234`

To monitor alerts in prometheus open port http 9090 of the docker host `http://<DOCKER-HOST IP-ADDRESS OR HOST-NAME>:9090/alerts` in browser

## Setup grafana with initial config
```
curl --location --request POST 'http://localhost:5601/api/saved_objects/_import' \
--header 'kbn-xsrf: true' \
--form 'file=@"./configs/kibana/02172022_kibana_backup.ndjson"'
```

### Display Metrics

Metrics are displayed at these URLs:

| Tool | Description | Connection Details |
| --- | --- | --- |
| [Grafana](http://localhost:3000) | Data displayed in dashboards | <ul> <li>URL: [http://localhost:3000](http://localhost:3000)</li><li>Username: admin</li><li>Password: secret1234</li></ul> |
| [FID-exporter](http://localhost:9095/metrics) | FID cn=monitor data | <ul> <li>URL: [http://localhost:9102/metrics](http://localhost:9095/metrics)</li></ul> |
| [cAdvisor](http://localhost:8080) | Container resource metrics | URL: [http://localhost:8080](http://localhost:8080) |
| [node-exporter](http://localhost:9100/metrics) | Raw node metrics | URL: [http://localhost:9100/metrics](http://localhost:9100/metrics) |
| [alertmanager](http://localhost:9093/#/alert) | Alerts displayed | URL: [http://localhost:9093/#/alerts](http://localhost:9093/#/alerts) |
| [Prometheus](https://localhost:9090) | Query collected data | URL: [https://localhost:9090](https://localhost:9090) |

> The Grafana dashboards correspond to the dashboard definitions in `configs/grafana/provisioning/dashboards`.

In Grafana, go to Dashboards -> Manage. The pre-populated dashboards with your live load results are displayed.


- To bring down and delete all the containers 
```
docker-compose down
```
> Note: Above command will not delete any volumes created while setting up container, Add `-v` flag to delete volumes as well `docker-compose down -v`

> Following usage command have been tested on docker version `20.10.8` & docker-compose version `1.29.2`




