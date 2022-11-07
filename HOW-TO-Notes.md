# How-TO notes

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

## Create registry access credentials secrets

[Ref](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/#create-a-secret-by-providing-credentials-on-the-command-line)

```sh
kubectl create secret docker-registry <regcred-name> \
--docker-server=<your-registry-server> \
--docker-username=<your-name> \
--docker-password=<your-pword> \
--docker-email=<your-email>
```

## Mount multiple config maps and secrets inside a given mounted volume

Hint: use ["projected" volumes](https://stackoverflow.com/questions/59855142/use-a-single-volume-to-mount-multiple-files-from-secrets-or-configmaps)