# How-TO notes

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