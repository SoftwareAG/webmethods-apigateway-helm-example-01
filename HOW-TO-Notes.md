# How-TO notes

- [How-TO notes](#how-to-notes)
  - [Deploy kubernetes dashboard](#deploy-kubernetes-dashboard)
  - [Kubernetes Secrets](#kubernetes-secrets)
    - [Create registry access credentials secrets](#create-registry-access-credentials-secrets)
    - [Create a secret from file](#create-a-secret-from-file)
  - [Mount multiple config maps and secrets inside a given mounted volume](#mount-multiple-config-maps-and-secrets-inside-a-given-mounted-volume)
  - [Testing with Docker Desktop](#testing-with-docker-desktop)
    - [Persistent volumes](#persistent-volumes)

## Deploy kubernetes dashboard

Detailed notes are [here.](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/)

Useful commands:

```sh
# install (once)
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.6.1/aio/deploy/recommended.yaml

# create dashboard service account (once)
kubectl create serviceaccount dashboard-admin-sa

# give permissions (once)
kubectl create clusterrolebinding dashboard-admin-sa --clusterrole=cluster-admin --serviceaccount=default:dashboard-admin-sa

# get access token for browser UI (as needed)
kubectl -n kubernetes-dashboard create token dashboard-admin-sa
```

## Kubernetes Secrets

### Create registry access credentials secrets

[Ref](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/#create-a-secret-by-providing-credentials-on-the-command-line)

```sh
kubectl create secret docker-registry <regcred-name> \
--docker-server=<your-registry-server> \
--docker-username=<your-name> \
--docker-password=<your-pword> \
--docker-email=<your-email>
```

### Create a secret from file

This is normally used for licenses

```sh
kubectl create secret generic <secret-name> \
--from-file=/path/to/license.key
```

## Mount multiple config maps and secrets inside a given mounted volume

Hint: use ["projected" volumes](https://stackoverflow.com/questions/59855142/use-a-single-volume-to-mount-multiple-files-from-secrets-or-configmaps)

## Testing with Docker Desktop

### Persistent volumes

In order to have dynamic provisioning of PVs, with Docker Desktop on WSL2, use the "hostpath" storageClassName in the PVC spec.
