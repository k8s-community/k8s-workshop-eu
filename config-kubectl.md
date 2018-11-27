# Setup the config

1. Store ca.crt data as a file, e.g. at your home directory. Remember its path, e.g. `~/k8scomm.ca.crt`.

2. Prepare the env variables and setup the configuration:
```
USER=your-github-user
TOKEN=your-token
CA_PATH=path-from-the-previous-step
```

3. Run the following commands to configure `kubectl` tool:
```
kubectl config set-cluster ws-${USER} \
    --embed-certs=true \
    --server=https://35.240.115.206 \
    --certificate-authority=${CA_PATH}
kubectl config set-credentials ws-${USER} --token=${TOKEN}
kubectl config set-context ws-${USER} \
    --cluster=ws-${USER} \
    --user=ws-${USER} \
    --namespace=${USER}
kubectl config use-context ws-${USER}
```

4. Check how it works:

```
kubectl get pods
```

As we haven't released anything yet, you will not see pods. But you shouldn't see any error either.
