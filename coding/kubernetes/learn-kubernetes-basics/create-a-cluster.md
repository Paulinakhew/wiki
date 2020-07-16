# Create a Cluster

{% embed url="https://kubernetes.io/docs/tutorials/kubernetes-basics/create-cluster/" caption="Documentation / Tutorials / Learn Kubernetes Basics / Create a Cluster" %}

## [Using Minikube to Create a Cluster](https://kubernetes.io/docs/tutorials/kubernetes-basics/create-cluster/cluster-intro/)

* **Kubernetes cluster:** a highly available cluster of computers that are connected to work as a single unit
* you can deploy an application to a cluster without tying them to a specific machine
* **containerizing** applications makes sure that they are packaged in a way that decouples them from individual hosts
  * containerized apps are more flexible and available than apps that are installed directly onto specific machines
* **Kubernetes automates the distribution and scheduling of application containers across a cluster in a more efficient way**
* a Kubernetes cluster consists of two types of resources:
  * the **Master** coordinates the cluster
  * **Nodes** are the workers that run applications



![Cluster diagram](../../../.gitbook/assets/image.png)

* **The master manages the cluster by coordinating all activities**
  * schedules applications
  * maintaining applications' desired state
  * scales applications
  * rolls out new updates
* **A node is a virtual machine \(VM\) or a physical computer that serves as a worker machine in a Kubernetes cluster**
  * each node has a **Kubelet,** an agent for managing the node and communicating with the Kubernetes master
  * the node should have tools for handling container operations
    * e.g. Docker or rkt
  * a Kubernetes cluster that handles production traffic should have a minimum of three nodes

> Masters manage the cluster and the nodes that are used to host the running applications.

* when deploying apps to Kubernetes, you tell the master to start the application containers
* the master schedules the containers to run on the cluster's nodes
* **the nodes communicate with the master using the** [**Kubernetes API**](https://kubernetes.io/docs/concepts/overview/kubernetes-api/)**,** which the master exposes
* end users can use the Kubernetes API directly to interact with the cluster



* a Kubernetes cluster can be deployed on either physical or virtual machines
* you can use **Minikube** to start with Kubernetes development

  * **Minikube:** a lightweight Kubernetes implementation that creates a VM on your local machine and deploys a simple cluster containing a single node
    * available for Linux, macOS, Windows
  * provides basic bootstrapping operations for working with your cluster
    * e.g. start, stop, status, delete

## [Interactive Tutorial: Creating a Cluster](https://kubernetes.io/docs/tutorials/kubernetes-basics/create-cluster/cluster-interactive/)

### Cluster up and running

`minikube version` - check that minikube is properly installed

```text
$ minikube version
minikube version: v1.8.1
commit: cbda04cf6bbe65e987ae52bb393c10099ab62014
```

`minikube start` - start the cluster

```text
$ minikube start
* minikube v1.8.1 on Ubuntu 18.04
* Using the none driver based on user configuration
* Running on localhost (CPUs=2, Memory=2460MB, Disk=145651MB) ...
* OS release is Ubuntu 18.04.4 LTS
* Preparing Kubernetes v1.17.3 on Docker 19.03.6 ...
  - kubelet.resolv-conf=/run/systemd/resolve/resolv.conf
* Launching Kubernetes ...
* Enabling addons: default-storageclass, storage-provisioner
* Configuring local host environment ...
* Waiting for cluster to come online ...
* Done! kubectl is now configured to use "minikube"
```

* once you run those commands, you'll have a running Kubernetes cluster in your online terminal
* Minikube started a VM that has a Kubernetes cluster running inside



### Cluster version

* you can use the **kubectl** command line interface to interact with Kubernetes

`kubectl version` - check if kubectl is installed

```text
$ kubectl version
Client Version: version.Info{Major:"1", Minor:"17", GitVersion:"v1.17.3", GitCommit:"06ad960bfd03b39c8310aaf92d1e7c12ce618213", GitTreeState:"clean", BuildDate:"2020-02-11T18:14:22Z", GoVersion:"go1.13.6", Compiler:"gc", Platform:"linux/amd64"}
Server Version: version.Info{Major:"1", Minor:"17", GitVersion:"v1.17.3", GitCommit:"06ad960bfd03b39c8310aaf92d1e7c12ce618213", GitTreeState:"clean", BuildDate:"2020-02-11T18:07:13Z", GoVersion:"go1.13.6", Compiler:"gc", Platform:"linux/amd64"}
```

* you can see both the client version and the server version once you run `kubectl version`
  * client version: kubectl version
  * server version: Kubernetes version installed on the master
* you can also see details about the build



### Cluster details

`kubectl cluster-info` - view the cluster details

```text
$ kubectl cluster-info
Kubernetes master is running at https://172.17.0.41:8443
KubeDNS is running at https://172.17.0.41:8443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
```

`kubectl get nodes` - view the nodes in the cluster

```text
$ kubectl get nodes
NAME       STATUS   ROLES    AGE     VERSION
minikube   Ready    master   3m13s   v1.17.3
```

* shows all nodes that can be used to host applications
* we have one node that is ready \(to accept applications for deployment\)



