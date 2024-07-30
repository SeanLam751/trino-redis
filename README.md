Trino Redis Helm Chart
==
This is a helm chart with the following features
- Trino with
    - 1 coordinator node
    - 2 worker nodes
    - A redis connector
- 2 Redis nodes
- 2 rocky linux nodes
- 1 ubuntu node with
    - Trino cli
    - Java 22 to run trino cli
- 1 python job to populate the redis node with data
## Usage
[Helm](https://helm.sh) must be installed to use the charts.

Once helm is installed, add the repo as follows:
```console
helm repo add trino-redis https://seanlam751.github.io/trino-redis/
```

To see the charts, run `helm search repo trino-redis`.

Then, you can install the chart with
```console
helm install trino-redis trino-redis/trino-redis
```
Trino may take 10 minutes to start-up.

Find {trino-svc-ip} by using `kubectl get svc trino-redis-trino` and looking at cluster-ip. Replace {trino-svc-ip} with the actual cluster ip.

To access trino using the command line interface, use the following commands
```
UBUNTU_POD_NAME=$(kubectl get pods --no-headers | grep 'ubuntu-deployment' | awk '{print $1}')
kubectl exec -it $UBUNTU_POD_NAME -- bin/bash
./trino --server {trino-svc-ip}:8080
```
To access keys and values from trino redis,
```
USE redis.default;
SELECT _key FROM "table";
SELECT _value FROM "table";
```
To access the web dashboard of trino, port forward the trino-redis service.
```
kubectl port-forward service/trino-redis-trino 8080:8080
```
