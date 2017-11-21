# Tarantool

[Tarantool](http://tarantool.io/) Tarantool is a Lua application server integrated with a database management system.

## Introduction

This chart bootstraps a [Tarantool](https://tarantool.org) deployment on a [Kubernetes](http://kubernetes.io) cluster
using the [Helm](https://helm.sh) package manager.

The chart is heavily based on [stable/redis](https://github.com/kubernetes/charts/tree/master/stable/redis) chart.

## Configuration

The following tables lists the configurable parameters of the Tarantool chart and their default values.

|           Parameter           |                Description                       |           Default            |
|-------------------------------|--------------------------------------------------|------------------------------|
| `image`                       | Tarantool image                                  | `tarantool/tarantool:1.8`    |
| `imagePullPolicy`             | Image pull policy                                | `IfNotPresent`               |
| `serviceType`                 | Kubernetes Service type                          | `ClusterIP`                  |
| `useSecurity`                 | Use password                                     | `false`                      |
| `tarantoolUser`               | Tarantool username                               | `tarantool`                  |
| `tarantoolPassword`           | Tarantool password                               | Randomly generated           |
| `args`                        | Tarantool command-line args                      | []                           |
| `persistence.enabled`         | Use a PVC to persist data                        | `true`                       |
| `persistence.existingClaim`   | Use an existing PVC to persist data              | `nil`                        |
| `persistence.storageClass`    | Storage class of backing PVC                     | `generic`                    |
| `persistence.accessMode`      | Use volume as ReadOnly or ReadWrite              | `ReadWriteOnce`              |
| `persistence.size`            | Size of data volume                              | `8Gi`                        |
| `resources`                   | CPU/Memory resource requests/limits              | Memory: `256Mi`, CPU: `100m` |
| `nodeSelector`                | Node labels for pod assignment                   | {}                           |
| `tolerations`                 | Toleration labels for pod assignment             | []                           |
| `networkPolicy.enabled`       | Enable NetworkPolicy                             | `false`                      |
| `networkPolicy.allowExternal` | Don't require client label for connections       | `true`                       |
| `service.annotations`         | annotations for tarantool service                | {}                           |
| `service.loadBalancerIP`      | loadBalancerIP if service type is `LoadBalancer` | ``                           |

The above parameters map to the env variables defined in [tarantool/tarantool](http://github.com/tarantool/docker).
For more information please refer to the [tarantool/tarantool](http://github.com/tarantool/docker) image documentation.

## Persistence

The [Tarantool](https://github.com/tarantool/docker) image stores the Tarantool data at the `/var/lib/tarantool` path of the container.

By default, the chart mounts a [Persistent Volume](http://kubernetes.io/docs/user-guide/persistent-volumes/) volume at this location.
The volume is created using dynamic volume provisioning. If a Persistent Volume Claim already exists, specify it during installation.

### Existing PersistentVolumeClaim

1. Create the PersistentVolume
1. Create the PersistentVolumeClaim
1. Install the chart
```bash
$ helm install --set persistence.existingClaim=PVC_NAME tarantool
```
