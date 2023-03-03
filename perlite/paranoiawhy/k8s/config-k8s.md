# `mysql`

切至 `config-k8s\k8s\mysql` :

```bash
kubectl create -f mysql-deployment.yaml
kubectl create -f mysql-persistent-volume-claim.yaml
kubectl create -f mysql-service.yaml
```

# `influxdb`

> [!tip] DOCKER_INFLUXDB_INIT_MODE
> `DOCKER_INFLUXDB_INIT_MODE` 的枚举值为:
> - `setup`
> - `upgrade`

切至 `config-k8s\k8s\influxdb` :

```bash
kubectl create -f influxdb.yaml
```

> [!info] kubectl create -f influxdb.yaml
> service/influxdb created
> statefulset.apps/influxdb created

`kubectl get pods` 查看到 `influxdb-0` 状态为 `pending` , 查看其报错信息:

```bash
kubectl describe pods influxdb-0
```

> [!warning] kubectl describe pods influxdb-0
> 0/1 nodes are available: 1 pod has unbound immediate PersistentVolumeClaims. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling.

[pod has unbound persistentvolumeclaims](https://stackoverflow.com/questions/52668938/pod-has-unbound-persistentvolumeclaims)

`influxdb.yaml` 中 `storageClassName` 修改为 `"hostpath"` 。

如果直接再次创建, 则会报错如下:

> [!error] kubectl create -f influxdb.yaml
> Error from server (AlreadyExists): error when creating "influxdb.yaml": services "influxdb" already exists
> Error from server (AlreadyExists): error when creating "influxdb.yaml": statefulsets.apps "influxdb" already exists

删除原有 `pods` :

```bash
kubectl delete pods influxdb-0
```

> [!info] kubectl delete pods influxdb-0
> pod "influxdb-0" deleted

上述命令删除的 `pods` 会自动重建(可通过 `kubectl get pods` 查看 `influxdb-0`), 因而需要删除以下内容:

```bash
kubectl delete service influxdb
kubectl delete statefulset influxdb
```

> [!info]
> service "influxdb" deleted
> statefulset.apps "influxdb" deleted

此时再次输入命令 `kubectl get pods` 可以看到 `influxdb-0` 已经不存在了。

或者:

```bash
kubectl delete -f influxdb.yaml

kubectl get pvc
kubectl delete pvc influxdb-influxdb-0
```

- `pv` 表示 `PersistentVolume`
- `pvc` 表示 `PersistentVolumeClaim`

- [Persistent Volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)

再次创建 `pods` :

```bash
kubectl create -f influxdb.yaml
```

查看 `service` 和 `statefulset` 信息:

```bash
kubectl get service influxdb
kubectl describe service influxdb

kubectl get statefulset influxdb
kubectl describe statefulset influxdb
```

# `rabbitmq`

切至 `config-k8s\k8s\rabbitmq\cluster\localhost` :

```bash
kubectl create -f cluster-operator.yaml
kubectl create -f rabbitmq.yaml
```

# `redis`

## `redis-cache`

切至 `config-k8s\k8s\redis-cache` :

```bash
kubectl create -f redis-deployment.yaml
kubectl create -f redis-service.yaml
```

> [!info]
> `kubectl create -f redis-deployment.yaml` :
> 
> configmap/cache-redis-config created
> deployment.apps/redis created
> 
> `kubectl create -f redis-service.yaml` :
> 
> service/redis created

## `redis-persist`

切至 `config-k8s\k8s\redis-persist` :

```bash
kubectl create -f persist-redis.yaml
```

> [!info] kubectl create -f persist-redis.yaml
> configmap/persist-redis-config created
> service/persist-redis created
> statefulset.apps/persist-redis created

# `zoo-keeper`

切至 `config-k8s\k8s\zoo-keeper` :

```bash
kubectl create -f zoo-keeper.yaml
```

> [!info] kubectl create -f zoo-keeper.yaml
> service/zk-cs created
> statefulset.apps/zk created
> error: resource mapping not found for name: "zk-pdb" namespace: "" from ".\\zoo-keeper.yaml": no matches for kind "PodDisruptionBudget" in version "policy/v1beta1"
> ensure CRDs are installed first

# `backend-api-data`

项目类型: **JAVA**

切至 `backend-api-data\k8s` :

```bash
docker tag backend-api-data gcr.io/cereb-platform-v2/backend-api-data:beta-jenkins-build.IMAGE_TAG_PLACEHOLDER

kubectl create -f deployment.yaml
kubectl create -f service.yaml
```

```yml
spec:
  ports:
  - name: "8080"
    port: 8080
    targetPort: 8080
    nodePort: 30000 # 30000-32767
  type: NodePort
  selector:
    io.kompose.service: api-data
```

# `backend-api-auth-center`

项目类型: **JAVA**

切至 `backend-api-auth-center\k8s` :

```bash
docker tag backend-api-auth-center gcr.io/cereb-platform-v2/backend-api-auth-center:beta-jenkins-build.IMAGE_TAG_PLACEHOLDER

kubectl create -f deployment.yaml
kubectl create -f service.yaml
```

构建镜像:

```bash
docker build -t gcr.io/cereb-platform-v2/backend-api-auth-center:beta-jenkins-build.IMAGE_TAG_PLACEHOLDER .
```

# `backend-api-gateway`

项目类型: **JAVA**

切至 `backend-api-gateway` :

```bash
docker tag backend-api-gateway gcr.io/cereb-platform-v2/backend-api-gateway:beta-jenkins-build.IMAGE_TAG_PLACEHOLDER

kubectl create -f service.yaml
kubectl create -f backendconfig.yaml
kubectl create -f deployment.yaml
```

# `backend-api-portal`

项目类型: **JAVA**

切至 `backend-api-portal` :

```bash
docker tag backend-api-portal gcr.io/cereb-platform-v2/backend-api-portal:beta-jenkins-build.IMAGE_TAG_PLACEHOLDER

kubectl create -f service.yaml
kubectl create -f deployment.yaml
```

