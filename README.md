# kluster

A tool that will generate docker compose files for custom Confluent Platform kafka clusters.

The output is ASCII text for a file that can be saved as `docker-compose.yml` then run with the command:

```
$ docker-compose up -d
```

The default cluster has a standalone Zookeeper, three kafka brokers, a variety of Confluent Platform 5.5.1 components in a single cluster. Use commandline arguments to override the defaults:

```
Usage:
  kluster [-v <CP version>] [-b <brokers>] [-r <racks>] [-c <clusters>] [options]
  kluster -h|--help

Options:
  -b <int>     Number of Apache Kafka brokers (default: 3, max: 9)
  -c           Number of clusters
  -d           Use ksqlDB instead of KSQL
  -k           Use Apache Kafka components only
  -j           Open JMX ports (only for cluster 1)
  -o           Exclude observibility containers 'control-center' and 'tools'
  -O           Include 'control-center' and 'tools'
  -r <int>     Number of racks or availability zones (default: none)
  -v <version> Confluent Platform version (default: 5.5.1)
  -z           Zookeeper 3 node ensemble (default: standalone)
  -Z <int>     Zookeeper ensemble with <int> nodes

Ports exposed on localhost:
  Zookeeper client  1000n
  Zookeeper admin   1008n
  Kafka client      10crb
  Zookeeper JMX     998n
  Kafka JMX         999n
  REST API ports    defaults + 10000

Mult-cluster Ports:
  Zookeeper are Control Center are shared between clusters
  Other components subtract 1000 for each cluster greater than 1

IDs:
  Zookeeper    n
  Broker ID  10n
  Rack ID    1n0
  Cluster ID n00
```

TCP/IP ports are opened to all interactions with external programs. The port numbers attempt to be non-conflicting so that you can reach all containers from `localhost` which is especially important when using macOS.



