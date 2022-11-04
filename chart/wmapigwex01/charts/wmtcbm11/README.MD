# Webmethods Terracotta Big Memory Server for API Gateway Helm Chart

This helm chart is inspired after the ones priveded by:

- [Sofware AG Government Solutions](https://github.com/softwareag-government-solutions/saggov-helm-charts/tree/main/src/webmethods-terracotta)
- [Software AG public example](https://github.com/SoftwareAG/webmethods-api-gateway/tree/master/samples/kubernetes/helm/cluster-deployment/apigateway/charts/terracotta)

## Local decisions

### One replica only

In this example the BigMemory server replicas are fixed to 1 as this type of deployment is more than sufficient for API Gateway. BigMemory servers are static by design and do not support elastic scalability as Kubernetes intends it. Therefore the deisgn choice is to have either one or two servers per stripe, and a stripe is more than sufficient for API Gateway.

In Kubernetes, a fast restart assures good enough availability of the service and the overall API Gateway cluster perfromance will be better as the BigMemory cluster sync does not exist, thus it does not intervene in the operations latency.

### Server must be restartable

The BigMemory Server MUST be restartable, otherwise the clients will have to be restarted too in case the server is restarted. This means the data volume must be mounted.

Additionally, we will also mount the logs folder and the backup folder.

The mountpoint must be considered as variables, because they depend on how the image was built. At the moment this repository is created, various builds with various mount points are available.

### Injecting configuration

Configuration injection will be done as specified in the officially provided container setup instructions [here](https://containers.softwareag.com/products/bigmemorymax-server)

In short, two files named exactly `license.key` and `tc-config.xml` must be present in readonly mode in the declared volume mountpoint `/opt/softwareag/config`.

Refer to [this](https://stackoverflow.com/questions/59855142/use-a-single-volume-to-mount-multiple-files-from-secrets-or-configmaps) article on how this is achieved in Kubernetes.
