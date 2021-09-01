# Accumulo

This repo contains Accumulo Helm chart for deploying on Kubernetes.

## Installation

Nodes where Accumulo needs to be deployed must be labeled. There are four labels, namely `accumulomaster` for master, `accumulotserver` for tserver, `accumulomonitor` for monitor and `accumulogc` for garbage collector. To label node use:

    $ kubectl label nodes node-list accumulomaster=true accumulotserver=true accumulomonitor=true accumulogc=true

Where:

 - `node-list` are nodes to label

To disable node selector just set `nodeselector` for monitor, master, tserver, and gc in `values.yaml` to `false`.  
Before installation fill `values.yaml` and to install Helm chart run:

    $ helm install some-chart-name --namespace=some-namespace-name --create-namespace path-to-chart-directory

Where:

- `some-chart-name` is Helm chart name
- `some-namespace-name` is optional argument that defines Kubernetes and Helm namespace where chart will be installed
- `path-to-chart-directory` is chart directory

## Values

Possible values to configure inside `values.yaml` are: 

 - `image` - defines Accumulo image name
 - `imageTag` - defines Accumulo image tag
 - `accumuloPassword` - defines Accumulo password for user `root`
 - `hadoopMasterAddress` - defines Hadoop namenode service name to connect
 - `zookeeperServiceName` - defines Zookeeper service name to connect
 - `replicas` - defines number of Pods (integer)
 - `nodeSelector` - defines node selector usage (boolean) and possible values are `true` and `false`
 - `nodePort` - defines service port where service can be accessed outside cluster

`Storage section` enables using costum volume mounts. To use it set `subsection enabled` to `true` and fill `volumeMounts` and `volumes` fields according to Kubernetes documentation.

## Uninstallation

To full uninstall run:

    $ helm del some-chart-name -n some-namespace-name

Where:

- `some-chart-name` is Helm chart name for uninstall.
- `some-namespace-name` is optional argument that defines Helm namespace where chart is installed.