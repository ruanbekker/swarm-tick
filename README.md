# swarm-telegraf-influxdb-chronograf-kapacitor

Monitor Swarm Cluster with Telegraf, InfluxDB, Chronograf, Kapacitor & Slack by [mlabouardy](https://github.com/mlabouardy/swarm-tig)

First of all thanks for [Mohamed Labouardy](https://github.com/mlabouardy/swarm-tig) for doing this.

## How to use it

* [Monitor Swarm cluster with TICK stack & Slack](https://hackernoon.com/monitor-swarm-cluster-with-tick-stack-slack-3aaa6483d44a)

## Template Variables:

Hosts:

![image](https://user-images.githubusercontent.com/567298/55782453-9ad47380-5aac-11e9-890d-cdb740773d83.png)

Containers:

![image](https://user-images.githubusercontent.com/567298/55782476-a9228f80-5aac-11e9-9677-697aedace99a.png)

## Dashboard Cells:

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
SELECT mean("tx_packets") AS "mean_tx_packets", mean("rx_packets") AS "mean_rx_packets" FROM "docker_metrics"."autogen"."docker_container_net_docker" WHERE time > :dashboardTime: AND "com.docker.swarm.service.name" = :container: GROUP BY :interval: FILL(null)
```

Query - IO Read/Write per Service

```
SELECT mean("io_serviced_recursive_write") AS "mean_io_recursive_write_write", mean("io_serviced_recursive_read") AS "mean_io_serviced_recursive_read" FROM "docker_metrics"."autogen"."docker_container_blkio_docker" WHERE time > :dashboardTime: AND "com.docker.swarm.service.name" = :container: GROUP BY :interval: FILL(null)
```


## Generate some load:

```
docker run --rm -it progrium/stress --vm 3 --timeout 500s
```

```
docker run --rm -it progrium/stress --cpu 4 --timeout 300s
```

## Screenshots:

![image](https://user-images.githubusercontent.com/567298/55853581-0f1d1e80-5b62-11e9-9b9e-361199ab3479.png)

![image](https://user-images.githubusercontent.com/567298/55853602-252adf00-5b62-11e9-8d3b-c54aabeb5fb2.png)

![image](https://user-images.githubusercontent.com/567298/55853615-3116a100-5b62-11e9-98f3-44abd2b5339b.png)

![image](https://user-images.githubusercontent.com/567298/55853644-4d1a4280-5b62-11e9-8a63-164e382b0383.png)

![image](https://user-images.githubusercontent.com/567298/55853728-a2eeea80-5b62-11e9-9e48-de9a72b7e505.png)


