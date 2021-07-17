# Changelog

## pre 1.0

### 0.3.3

* added support for disabling liveness- and readinessProbe
* added support for customLivenessProbd and customReadinessProbe
* added support for securityContext configuration via values.yaml
* added support for service type LoadBalancer and loadBalancerIP
* added support for directories
* added support for extraVolumes and extraVolumeMounts
* updated documentation

### 0.3.2

* add .helmignore for a clean chart

### 0.3.1

* Move debug container to first position to make it the default target for container attachments.
* Fix inclusion of resource definitions.

### 0.3.0

* Added `NET_ADMIN` capabilities to the sftp-server container.
* Added nettools-debug containers (disabled by default)
* Changed sftp resource-definition from .resources to resources.sftp

### 0.2.0

* change update strategy to `Recreate` to prevent deadlock on PV allocation

### 0.1.1

* change image repository to `quay.io/openvnf/sftp`
