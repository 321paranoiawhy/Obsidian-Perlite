#k8s #Getting-Started
- 基于容器的集群管理平台
- [kubernetes.io](https://kubernetes.io/)
- `kubernetes` 源自希腊语, 本意为**舵手**或**领航员**
- `k8s` 中的 `8`表示首字母 `k` 和尾字母 `s` 之间的 `8` 个字符 `ubernete`

`k8s` 集群, 一个主节点负责管理和控制 (`Master`), 多个计算节点 (`Node`)

微服务架构 (`Microservices`)

> [!note]
> 容器编排技术:
> - [Swarm](https://docs.docker.com/engine/swarm/)
> - [MESOS](https://mesos.apache.org/)
> - [kubernetes.io](https://kubernetes.io/)

# 配置自动补全

- [bash](https://kubernetes.io/docs/reference/kubectl/cheatsheet/#bash)
- [zsh](https://kubernetes.io/docs/reference/kubectl/cheatsheet/#zsh)
- [Make PowerShell with k8s great again](https://stapp.space/pskube-context/)
- [PowerShell auto-completion for kubectl - GitHub](https://github.com/mziyabo/PSKubectlCompletion)
- [PSKubectlCompletion - Kubectl auto-completion for PowerShell](https://www.powershellgallery.com/packages/PSKubectlCompletion/1.0.4)
- [PowerShell kubectl autocomplete](https://mziyabo.co/2020/kubectl-auto-completion-in-powershell/)
- [optional kubectl configs pwsh - 404](https://kubernetes.io/docs/tasks/tools/included/optional-kubectl-configs-pwsh/)

```bash
Install-Module -Name PSKubectlCompletion
```

打开 `Microsoft.PowerShell_profile.ps1` 配置文件并加入以下内容:

```txt
Import-Module -Name PSKubectlCompletion
```

# 各种 `port`

- [Kubernetes -- port, targetport, nodeport的区别](http://sonicguo.com/2020/k8s-port-targetport-nodeport/)
- [Kubernetes - Port，Targetport 和 NodePort的关系](https://segmentfault.com/a/1190000020400286)

## `port`

## `targetPort`

## `nodePort`

## `containerPort`

# 查看内存占用

```bash
kubectl top nodes
```

也可使用 `docker stats <Container Name>/<Container ID>` 命令。

查看各 `pod` 详细信息:

```bash
k8s get pods -o wide
```

# 获取 `nodes`

```bash
kubectl get nodes
```

|      NAME      | STATUS |     ROLES     | AGE | VERSION |
|:--------------:|:------:|:-------------:|:---:|:-------:|
| docker-desktop | Ready  | control-plane | 44h | v1.25.4 |

```bash
k8s describe node docker-desktop
```

| Resource          | Requests     | Limits        |
|:-----------------:|:------------:|:-------------:|
| cpu               |  2600m (43%) | 16200m (270%) |
| memory            | 5824Mi (99%) | 9800Mi (167%) |
| ephemeral-storage |       0 (0%) |        0 (0%) |
| hugepages-1Gi     |       0 (0%) |        0 (0%) |
| hugepages-2Mi     |       0 (0%) |        0 (0%) |

# 命令缩写

- [Resource types and abbreviated aliases](https://kubernetes.io/docs/reference/kubectl/#resource-types)

|         原命令         | 命令缩写 |
| :--------------------: | :------: |
|         nodes          |    no    |
|   persistentvolumes    |    pc    |
| persistentvolumeclaims |   pvc    |
|          pods          |    po    |
|        services        |   svc    |
|      deployments       |  deploy  |
|      statefulsets      |   sts    |
|         events         |    ev    |
|     storageclasses     |    sc    |

# 常用命令

- [Command line tool (kubectl)](https://kubernetes.io/docs/reference/kubectl/)
- [minikube start](https://minikube.sigs.k8s.io/docs/start/)
- [kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

## 查看 `k8s` 版本

```bash
kubectl version
kubectl version --short
```

> [!info] kubectl version --short
> Flag --short has been deprecated, and will be removed in the future. The --short output will become the default.
> Client Version: v1.25.4  
> Kustomize Version: v4.5.7
> Server Version: v1.25.4

`Client Version` 表示 `kubernetes` 版本信息, `Server Version` 表示 `master` 节点的 `k8s` 版本信息。

## 查看 `k8s` 帮助

```bash
kubectl --help
```

> [!info]- kubectl --help
> kubectl controls the Kubernetes cluster manager.
> 
>  Find more information at: https://kubernetes.io/docs/reference/kubectl/
> 
> Basic Commands (Beginner):
>   create          Create a resource from a file or from stdin
>   expose          Take a replication controller, service, deployment or pod and expose it as a new Kubernetes service
>   run             Run a particular image on the cluster
>   set             Set specific features on objects
> 
> Basic Commands (Intermediate):
>   explain         Get documentation for a resource
>   get             Display one or many resources
>   edit            Edit a resource on the server
>   delete          Delete resources by file names, stdin, resources and names, or by resources and label selector
> 
> Deploy Commands:
>   rollout         Manage the rollout of a resource
>   scale           Set a new size for a deployment, replica set, or replication controller
>   autoscale       Auto-scale a deployment, replica set, stateful set, or replication controller
> 
> Cluster Management Commands:
>   certificate     Modify certificate resources.
>   cluster-info    Display cluster information
>   top             Display resource (CPU/memory) usage
>   cordon          Mark node as unschedulable
>   uncordon        Mark node as schedulable
>   drain           Drain node in preparation for maintenance
>   taint           Update the taints on one or more nodes
> 
> Troubleshooting and Debugging Commands:
>   describe        Show details of a specific resource or group of resources
>   logs            Print the logs for a container in a pod
>   attach          Attach to a running container
>   exec            Execute a command in a container
>   port-forward    Forward one or more local ports to a pod
>   proxy           Run a proxy to the Kubernetes API server
>   cp              Copy files and directories to and from containers
>   debug           Create debugging sessions for troubleshooting workloads and nodes
> 
> Advanced Commands:
>   diff            Diff the live version against a would-be applied version
>   apply           Apply a configuration to a resource by file name or stdin
>   patch           Update fields of a resource
>   replace         Replace a resource by file name or stdin
>   wait            Experimental: Wait for a specific condition on one or many resources
>   kustomize       Build a kustomization target from a directory or URL.
> 
> Settings Commands:
>   label           Update the labels on a resource
>   annotate        Update the annotations on a resource
>   completion      Output shell completion code for the specified shell (bash, zsh, fish, or powershell)
> 
> Other Commands:
>   alpha           Commands for features in alpha
>   api-resources   Print the supported API resources on the server
>   api-versions    Print the supported API versions on the server, in the form of "group/version"
>   config          Modify kubeconfig files
>   plugin          Provides utilities for interacting with plugins
>   version         Print the client and server version information
> 
> Usage:
>   kubectl [flags] [options]
> 
> Use "kubectl <command> --help" for more information about a given command.
> Use "kubectl options" for a list of global command-line options (applies to all commands).

## 查看 `k8s` 运行状态

```bash
kubectl cluster-info
```

> [!info] kubectl cluster-info
> Kubernetes control plane is running at https://kubernetes.docker.internal:6443
> CoreDNS is running at https://kubernetes.docker.internal:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
> 
> To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.

## 发布到 `k8s`

切至 `config-k8s\k8s\mysql` :

```bash
kubectl create -f mysql-deployment.yaml
kubectl create -f mysql-persistent-volume-claim.yaml
kubectl create -f mysql-service.yaml
```

> [!info] kubectl create -f mysql-deployment.yaml
> deployment.apps/mysql created

## 查看 `pods`

查看所有 `pods` :

```bash
kubectl get pods
```

查看所有 `pods` 详细信息:

```bash
kubectl describe pods
```

查看指定 `pods` 详细信息:

```bash
kubectl describe pods <pod-name>
```

查看指定 `pods` 日志:

```bash
kubectl logs <pod-name>
```

## 获取 `k8s` 的上下文指向

获取当前的 `k8s` 上下文指向:

```bash
kubectl config current-context
```

![[../Attachments/Kubernetes-current-context.png]]

> [!tip]
> 在任务栏中右键 `Docker` 图标, 可以看到顶部的两条信息 `Docker Desktop is running` 和 `Kubernetes is running`, 并且鼠标悬浮至 `Kubernetes` 可看到其上下文指向, 如 `docker-desktop` 。

获取 `k8s` 可用的上下文指向:

```bash
kubectl config get-contexts
```

设置 `k8s` 的上下文指向:

```bash
kubectl config use-context my-cluster-name
```

- [Use the kubectl command](https://docs.docker.com/desktop/kubernetes/#use-the-kubectl-command)

## 获取 `k8s` 的节点

```bash
kubectl get nodes
```

> [!info] kubectl get nodes
> NAME             STATUS   ROLES           AGE    VERSION
> docker-desktop   Ready    control-plane   144m   v1.25.4

## 获取命名空间

```bash
kubectl get namespaces
```

> [!info] kubectl get namespaces
> NAME              STATUS   AGE 
> default           Active   125m
> kube-node-lease   Active   125m
> kube-public       Active   125m
> kube-system       Active   125m
