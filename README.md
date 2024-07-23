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