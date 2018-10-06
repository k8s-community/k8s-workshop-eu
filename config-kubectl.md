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
    --server=kubernetes \
    --certificate-authority=${CA_PATH}
kubectl config set-credentials ws-${USER} --token=${TOKEN}
kubectl config set-context ws-${USER} \
    --cluster=ws-${USER} \
    --user=ws-${USER}
kubectl config use-context ws-${USER}
```

4. As we are going to make requests to https://kubernetes, we need to identify the real host for this hostname:

```
echo '35.187.39.10 kubernetes' | sudo tee -a /etc/hosts
```

(Please, don't forget to remove this line from `/etc/hosts` after the workshop)

4. Check how it works:

```
kubectl get pods -n ${USER}
```

As we haven't released anything yet, you will not see pods. But you shouldn't see any error either.
