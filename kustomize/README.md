# Kustomize

Kustomize for Spark cluster with Jupyter Lab

## Requirements

[Kustomize](https://github.com/kubernetes-sigs/kustomize) is required for creating Spark cluster here.

## Usage

Build kubernetes manifests by kustomize, then apply by kubectl.

```sh
kustomize build . | kubectl apply -f -
```

### Use Spark in kubernetes cluster

You can access Jupyter Lab `https://jupyter-lab.localhost` running on kubernetes.
You can use SparkSession simply.

```py
from pyspark.sql import SparkSession


spark = SparkSession.builder.getOrCreate()
```

### Use Spark from your local machine

If you wanted to use from your local machine, you should specify at least `spark master`, `executor image` and `namespace`.
Master is kubernetes api server URL. You can check by kubectl.

```sh
kubectl cluster-info
```

Maybe following environment variables is should be set.
Python version must be same `PYSPARK_DRIVER_PYTHON` and `PYSPARK_PYTHON`.

```sh
export PYSPARK_DRIVER_PYTHON=/path/to/your/local/python
# PATH to python in docker image for executor (kanchishimono/pyspark)
export PYSPARK_PYTHON=/opt/.pyenv/shims/python
```

Then you can get SparkSession from your local machine.

```py
from pyspark.sql import SparkSession


spark = (
    SparkSession
    .builder
    .master('k8s://https://<kubernetes-master-ip>:<kubernetes-master-port>')
    .config('spark.kubernetes.container.image', 'kanchishimono/pyspark:master')
    .config('spark.kubernetes.namespace', 'spark')
    .getOrCreate()
)
```
