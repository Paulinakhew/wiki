---
description: 'Pods, Nodes, Kubectl main commands'
---

# Explore Your App

{% embed url="https://kubernetes.io/docs/tutorials/kubernetes-basics/explore/" caption="Documentation / Tutorials / Learn Kubernetes Basics / Explore Your App" %}

## [Viewing Pods and Nodes](https://kubernetes.io/docs/tutorials/kubernetes-basics/explore/explore-intro/)

### Kubernetes Pods

* **pod:** a Kubernetes abstraction that represents one or more application containers \(e.g. Docker or rkt\) and some shared resources for those containers
  * hosts your application instance
* Resources include:
  * shared storage, as Volumes
  * networking, as a unique cluster IP address
  * information about how to run each container \(e.g. the container image version or specific ports to use\)
* a Pod models an application-specific "logical host"
  * **logical host:** a logical server environment that acts as the execution environment
  * can contain different application containers that are tightly coupled
    * e.g. it might include a container with your Node.js app and a different container that feeds the data to be published by the Node.js webserver
* the containers in a Pod share an IP Address and port ~~s~~pace
  * containers are co-located and co-scheduled
  * run in a shared context on the same Node
* pods are the atomic unit on Kubernetes
* a Deployment on Kubernetes creates Pods with containers inside them \(as opposed to creating containers directly\)
* each Pod is tied to the Nod where it is scheduled
  * remains there until termination or deletion
* if a Node fails, identical Pods are scheduled on other available Nodes in the cluster

![Pods Overview](../../../.gitbook/assets/image%20%284%29.png)



### Nodes

* a Pod always runs on a **Node**
* **node:** a worker machine in Kubernetes that can be a virtual or physical machine, depending on the cluster
  * nodes are managed by the Master
  * can have multiple pods
* Kubernetes master automatically handles scheduling pods across Nodes in the cluster
* the Master's automatic scheduling takes into account the available resources on each Node
* each k8s Node runs at least:
  * Kubelet: a process responsible for communication between the Master and the Node
    * manages the Pods and the containers running on a machine
  * a container runtime \(e.g. Docker, rkt\) that pulls the container image from a registry, unpacks the container, and runs the application

![Node overview](../../../.gitbook/assets/image%20%283%29.png)



### Troubleshooting with kubectl

* the following are common operations that can be done with kubectl:
  * `kubectl get` - list resources
  * `kubectl describe` - show detailed information about a resource
  * `kubectl logs` - print the logs from a container in a pod
  * `kubectl exec` - execute a command from a container in a pod
* you can use these commands to see when applications were deployed, what their current statuses are, where they are running and what their configurations are



## [Interactive Tutorial - Exploring Your App](https://kubernetes.io/docs/tutorials/kubernetes-basics/explore/explore-interactive/)

### Check application configuration

`kubectl get pods` - look for existing pods

```text
$ kubectl get pods
NAME                                   READY   STATUS    RESTARTS AGE
kubernetes-bootcamp-765bf4c7b4-2csd9   1/1     Running   0 16s
```

* if no pods are running, it means the interactive environment is still reloading its previous state
  * wait a few seconds and list the Pods again

`kubectl describe pods` - view what containers are inside the Pod and what images are used to build the containers

```text
$ kubectl describe pods
Name:         kubernetes-bootcamp-765bf4c7b4-2csd9
Namespace:    default
Priority:     0
Node:         minikube/172.17.0.21
Start Time:   Fri, 17 Jul 2020 15:21:02 +0000
Labels:       pod-template-hash=765bf4c7b4
              run=kubernetes-bootcamp
Annotations:  <none>
Status:       Running
IP:           172.18.0.5
IPs:
  IP:           172.18.0.5
Controlled By:  ReplicaSet/kubernetes-bootcamp-765bf4c7b4
Containers:
  kubernetes-bootcamp:
    Container ID:   docker://f0c94d70ca26da1cc4c8e5944d0a6cdab5085e573bf656ab86fb7f8d2851e434
    Image:          gcr.io/google-samples/kubernetes-bootcamp:v1
    Image ID:       docker-pullable://jocatalin/kubernetes-bootcamp@sha256:0d6b8ee63bb57c5f5b6156f446b3bc3b3c143d233037f3a2f00e279c8fcc64af
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Fri, 17 Jul 2020 15:21:06 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-2q245 (ro)
Conditions:
  Type              Status
  Initialized       True
  Ready             True
  ContainersReady   True
  PodScheduled      True
Volumes:
  default-token-2q245:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-2q245
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type     Reason            Age                    From    Message
  ----     ------            ----                   ----    -------
  Warning  FailedScheduling  2m33s (x2 over 2m33s)  default-scheduler  0/1 nodes are available: 1 node(s) had taints that the pod didn't tolerate.
  Normal   Scheduled         2m27s                  default-scheduler  Successfully assigned default/kubernetes-bootcamp-765bf4c7b4-2csd9 to minikube
  Normal   Pulled            2m24s                  kubelet, minikube  Container image "gcr.io/google-samples/kubernetes-bootcamp:v1"already present on machine
  Normal   Created           2m23s                  kubelet, minikube  Created container kubernetes-bootcamp
  Normal   Started           2m22s                  kubelet, minikube  Started container kubernetes-bootcamp
```

* you can see details about the Pod's container:
  * IP addres
  * ports used
  * list of events related to the life cycle of the pod

> _Note: the describe command can be used to get detailed information about most of the kubernetes primitives: node, pods, deployments. The describe output is designed to be human readable, not to be scripted against._

### Show the app in the terminal

* pods run in an isolated, private network so you need proxy access to debug and interact with them
* use the `kubectl proxy` command to run a proxy in a second terminal window

`kubectl proxy` - run the proxy

```text
Starting to serve on 127.0.0.1:8001
```

* again, we need to get the Pod name and query the pod through the proxy

`export POD_NAME=$(kubectl get pods -o go-template --template '')`  
`echo Name of the Pod: $POD_NAME`

```text
$ export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}')
$ echo Name of the Pod: $POD_NAME
Name of the Pod: kubernetes-bootcamp-765bf4c7b4-2csd9
```

* to see the output of the application, you can use `curl`

`curl` 

