# exporter

## Setup
#### Prometheus
**An existing prometheus server is required to use this project**

To learn more about how to setup promethues and grafana see: https://eksworkshop.com/monitoring/

#### Grafana
The dashboard pictured above is [available to download from grafana](https://grafana.com/grafana/dashboards/10128).
It will work aslong as EXPORTER_STAT_PREFIX is not changed.

## Queue Discovery
Queues are discovered at start up by running `KEYS bull:*:id` 
this can also be triggered manually from the `/discover_queues` endpoint
`curl -XPOST localhost:9538/discover_queues`

## Metrics

| Metric                       | type    | description |
|------------------------------|---------|-------------|
| bull_queue_completed         | counter | Total number of completed jobs                          |
| bull_queue_complete_duration | summary | Processing time for completed jobs                      |
| bull_queue_active            | counter | Total number of active jobs (currently being processed) |
| bull_queue_delayed           | counter | Total number of jobs that will run in the future        |
| bull_queue_failed            | counter | Total number of failed jobs                             |
| bull_queue_waiting           | counter | Total number of jobs waiting to be processed            |

## Kubernetes Usage

### Environment variables for default docker image

| variable              | default                  | description                                     |
|-----------------------|--------------------------|-------------------------------------------------|
| EXPORTER_REDIS_URL    | redis://localhost:6379/0 | Redis uri to connect                            |
| EXPORTER_PREFIX       | bull                     | prefix for queues                               |
| EXPORTER_STAT_PREFIX  | bull_queue_              | prefix for exported metrics                     |
| EXPORTER_QUEUES       | -                        | a space separated list of queues to check       |
| EXPORTER_AUTODISCOVER | -                        | set to '0' or 'false' to disable queue discovery|

