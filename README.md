# Introduction
This chart bootstraps an emqx deployment on a Kubernetes cluster using the Helm package manager. 

# Prerequisites
+ Kubernetes 1.6+
+ Helm

# Installing the Chart
To install the chart with the release name `my-emqx`:

+   From github 
    ```
    $ git clone https://github.com/emqx/emqx-rel.git
    $ cd emqx-rel/deploy/charts/emqx
    $ helm install my-emqx .
    ```

+   From chart repos
    ```
    helm repo add emqx https://repos.emqx.io/charts
    helm install my-emqx emqx/emqx
    ```
    > If you want to install an unstable version, you need to add `--devel` when you execute the `helm install` command.

# Uninstalling the Chart
To uninstall/delete the `my-emqx` deployment:
```
$ helm del  my-emqx
```

# Configuration
The following table lists the configurable parameters of the emqx chart and their default values.

| Parameter  | Description | Default Value |
| ---        |  ---        | ---           |
| `replicaCount` | It is recommended to have odd number of nodes in a cluster, otherwise the emqx cluster cannot be automatically healed in case of net-split. |3|
| `image.repository` | EMQ X Image name |emqx/emqx|
| `image.pullPolicy`  | Global Docker registry secret names as an array |IfNotPresent|
| `persistence.enabled` | Enable EMQX persistence using PVC |false|
| `persistence.storageClass` | Storage class of backing PVC |`nil` (uses alpha storage class annotation)|
| `persistence.existingClaim` | EMQ X data Persistent Volume existing claim name, evaluated as a template |""|
| `persistence.accessMode` | PVC Access Mode for EMQX volume |ReadWriteOnce|
| `persistence.size` | PVC Storage Request for EMQX volume |20Mi|
| `resources` | CPU/Memory resource requests/limits |{}|
| `nodeSelector` | Node labels for pod assignment |`{}`|
| `tolerations` | Toleration labels for pod assignment |`[]`|
| `affinity` | Map of node/pod affinities |`{}`|
| `service.type`  | Kubernetes Service type. |ClusterIP|
| `service.mqtt`  | Port for MQTT. |1883|
| `service.mqttssl` | Port for MQTT(SSL). |8883|
| `service.mgmt`  | Port for mgmt API. |8081|
| `service.ws`  | Port for WebSocket/HTTP. |8083|
| `service.wss`  | Port for WSS/HTTPS. |8084|
| `service.dashboard`  | Port for dashboard. |18083|
| `service.nodePorts.mqtt`  | Kubernetes node port for MQTT. |nil|
| `service.nodePorts.mqttssl` | Kubernetes node port for MQTT(SSL). |nil|
| `service.nodePorts.mgmt`  | Kubernetes node port for mgmt API. |nil|
| `service.nodePorts.ws`  | Kubernetes node port for WebSocket/HTTP. |nil|
| `service.nodePorts.wss`  | Kubernetes node port for WSS/HTTPS. |nil|
| `service.nodePorts.dashboard`  | Kubernetes node port for dashboard. |nil|
| `service.loadBalancerIP`  | loadBalancerIP for Service |	nil |
| `service.loadBalancerSourceRanges` |	Address(es) that are allowed when service is LoadBalancer |	[] |
| `service.annotations` |	Service annotations |	{}(evaluated as a template)|
| `emqxConfig` | Emqx configuration item, see the [documentation](https://hub.docker.com/r/emqx/emqx-ee) | |
| `emqxAclConfig` | Emqx acl configuration item, see the [documentation](https://docs.emqx.io/broker/latest/en/advanced/acl-file.html) | |
| `emqxLicneseSecretName` | EMQX Enterprise Edition requires manual creation of a Secret containing the licensed content. Write the name of Secret to the value of "emqxLicneseSecretName" | "" |
