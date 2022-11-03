# WebMethods API Gateway Solution 01 Helm Chart

- [WebMethods API Gateway Solution 01 Helm Chart](#webmethods-api-gateway-solution-01-helm-chart)
  - [Description](#description)
  - [How-tos](#how-tos)
    - [How to: create registry access credentials secrets](#how-to-create-registry-access-credentials-secrets)

## Description

"Solution 01" separates the components of API Gateway in dedicated deployments as in the following diagram:

![Architecture Overview](architecture.svg)

## How-tos

### How to: create registry access credentials secrets

[Ref](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/#create-a-secret-by-providing-credentials-on-the-command-line)

```sh
kubectl create secret docker-registry <regcred-name> \
--docker-server=<your-registry-server> \
--docker-username=<your-name> \
--docker-password=<your-pword> \
--docker-email=<your-email>
```
