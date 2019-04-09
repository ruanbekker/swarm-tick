# swarm-tick

Monitor Swarm Cluster with Telegraf, InfluxDB, Chronograf, Kapacitor & Slack


## How to use it

* [Monitor Swarm cluster with TICK stack & Slack](https://hackernoon.com/monitor-swarm-cluster-with-tick-stack-slack-3aaa6483d44a)


Query - Memory Usage per Node:

```
SELECT mean("free") AS "mean_free", mean("used") AS "mean_used", mean("total") AS "mean_total" FROM "vm_metrics"."autogen"."mem_vm" WHERE time > :dashboardTime: AND "host"=:host: GROUP BY :interval: FILL(null)
```

Query - CPU Usage per Node:

```
SELECT mean("usage_user") AS "mean_usage_user", mean("usage_system") AS "mean_usage_system" FROM "vm_metrics"."autogen"."cpu_vm" WHERE time > :dashboardTime: AND "host"=:host: GROUP BY :interval: FILL(null)
```

Query - Disk Usage per Node:

```
SELECT mean("free") AS "mean_free", mean("total") AS "mean_total", mean("used") AS "mean_used" FROM "vm_metrics"."autogen"."disk_vm" WHERE time > :dashboardTime: AND "host"=:host: GROUP BY :interval: FILL(null)
```

Query - Memory Usage per Service:

```
SELECT mean("usage_percent") AS "mean_usage_percent" FROM "docker_metrics"."autogen"."docker_container_mem_docker" WHERE time > :dashboardTime: AND "com.docker.swarm.service.name" = :container: GROUP BY :interval: FILL(null)
```

Query - CPU Per Service:

```
SELECT mean("usage_percent") AS "mean_usage_percent" FROM "docker_metrics"."autogen"."docker_container_cpu_docker" WHERE time > :dashboardTime: AND "com.docker.swarm.service.name" = :container: GROUP BY :interval: FILL(null)
```

Query - Network Transmit Receive:

```
SELECT mean("tx_packets”) AS "mean_tx_packets", mean("rx_packets") AS "mean_rx_packets" FROM "docker_metrics"."autogen"."docker_container_net_docker" WHERE time > :dashboardTime: AND "com.docker.swarm.service.name" = :container: GROUP BY :interval: FILL(null)
```

Query - IO Read/Write per Service

```
SELECT mean("io_serviced_recursive_write") AS "mean_io_recursive_write_write", mean("io_serviced_recursive_read") AS "mean_io_serviced_recursive_read" FROM "docker_metrics"."autogen"."docker_container_blkio_docker" WHERE time > :dashboardTime: AND “com.docker.swarm.service.name” = :container: GROUP BY :interval: FILL(null)
```

## Maintainers
* Mohamed Labouardy - mohamed@labouardy.com
