# SFTP Server

A helm chart for a SFTP server.


## Introduction

The SFTP server is based on [atmoz/sftp](https://github.com/atmoz/sftp).

The chart supports:
- persistent SSH server host keys
- provision of authorized SSH keys
- persistentVolumeClaim for data
- [kube-vxlan-controller](https://github.com/openvnf/kube-vxlan-controller)


## Prerequisites

- Kubernetes 1.6+ with Beta APIs enabled


## Installing the Chart

To install the chart with the release name `my-release`:

```bash
$ helm install --name my-release repo/sftp-server
```

The command deploys an SFTP server exposing the service as `ClusterIP`. The [configuration](#configuration) section lists the parameters that can be configured during installation.


## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```bash
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the SFTP server chart and their default values.

|          Parameter                 |                Description                 |                   Default                   |
| -----------------------------------| ------------------------------------------ | ------------------------------------------- |
| `image.repository`                 | Docker repo to use                         | `atmoz/sftp`                                |
| `image.tag`                        | Docker tag to be used                      | `alpine-3.7`                                |
| `image.pullPolicy`                 | Image pull policy                          | `IfNotPresent`                              |
| `service.enabled`                  | If true, expose as Service                 | `true`                                      |
| `service.type`                     | Type of exposed Service                    | `ClusterIP`                                 |
| `service.port`                     | Port to expose Service                     | `22`                                        |
| `service.loadBalancerIP`           | Specific IP for type LoadBalancer          | `""`                                        |
| `sftp.securityContext`             | Set security context for sftp container    | `NET_ADMIN`                                 |
| `sftp.extraVolumeMounts`           | extra volumeMounts for the sftp container  | `""`                                        |
| `sftp.livenessProbe`               | enable/disable livenessProbe               | `true`                                        |
| `sftp.readinessProbe`              | enable/disable readinessProbe              | `true`                                        |
| `sftp.customLivenessProbe`         | specify a custom livenessProbe             | `""`                                        |
| `sftp.customReadinessProbe`        | specify a custom readinessProbe            | `""`                                        |
| `sftpConfig.username`              | SFTP username                              | `sftp`                                      |
| `sftpConfig.password`              | SFTP password for user                     | `""`                                        |
| `sftpConfig.encrypted`             | If true, password is given as hash         | `false`                                     |
| `sftpConfig.uid`                   | UID of SFTP user                           | `1000`                                      |
| `sftpConfig.gid`                   | GID of SFTP user                           | `100`                                       |
| `sftpConfig.dirs`                  | Directories of SFTP user                   | `""`                                        |
| `sftpConfig.hostKeys.secret`       | name of secret for SSH host keys           | `""`                                        |
| `sftpConfig.hostKeys.keys`         | list of items to be used from secret       | `{}`                                        |
| `sftpConfig.authorizedKeys`        | list of authorized SSH keys                | `{}`                                        |
| `persistentVolume.enabled`         | If true, use persistent volume             | `true`                                      |
| `persistentVolume.annotations`     | annotations put on the volume              | `{}`                                        |
| `persistentVolume.accessModes`     | access modes for volume                    | `[ReadWriteOnce]`                           |
| `persistentVolume.existingClaim`   | If set, use existing PVC                   | `""`                                        |
| `persistentVolume.size`            | Size of volume                             | `20Gi`                                      |
| `persistentVolume.storageClass`    | StorageClass to be used in PVC             | not set                                     |
| `persistentVolume.subPath`         | Use subPath of existing volume             | `""`                                        |
| `extraVolumes`                     | extra volumes for the sftp deployment      | `""`                                        |
| `vxlanController.enabled`          | If enabled, start kube-vxlan-controller    | `false`                                     |
| `vxlanController.annotationKey`    | Annotation name to set for vxlan           | `vxlan.openvnf.org/networks`                |
| `vxlanController.metadataKey`      | Metadata key to set for vxlan              | `vxlan.openvnf.org`                         |
| `vxlanController.image.repository` | Docker repo to use                         | `openvnf/kube-vxlan-controller-agent`       |
| `vxlanController.image.tag`        | Docker tag to be used                      | `2.1.0`                                     |
| `vxlanController.image.pullPolicy` | Image pull policy                          | `IfNotPresent`                              |
| `vxlanController.network`          | VXLAN network to attach to                 | `vxeth0`                                    |
| `vxlanController.ip`               | IP address to assign to vxlan interface    | `{}`                                        |
| `vxlanController.route`            | additional route to configure              | `{}`                                        |
