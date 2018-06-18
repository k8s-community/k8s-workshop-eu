# Setup the config

1. Store ca.crt data as a file, e.g. at your home directory. Remember its path, e.g. `~/cdays.ca.crt`.

2. Prepare the env parameters and setup the configuration:
```
USER=your-github-user
TOKEN=your-token
CA_PATH=path-from-the-previous-step
```

3. Run the following commands to configure `kubectl` tool:
```
kubectl config set-cluster cdays-${USER} \
    --embed-certs=true \
    --server=https://35.230.108.61 \
    --certificate-authority=${CA_PATH}
kubectl config set-credentials cdays-${USER} --token=${TOKEN}
kubectl config set-context cdays-${USER} \
    --cluster=cdays-${USER} \
    --user=cdays-${USER}
kubectl config use-context cdays-${USER}
```

4. Check how it works:

```
kubectl get pods -n ${USER}
```
