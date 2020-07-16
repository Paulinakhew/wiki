---
description: 'Pods, Nodes, Kubectl main commands'
---

# Explore Your App

{% embed url="https://kubernetes.io/docs/tutorials/kubernetes-basics/explore/" caption="Documentation / Tutorials / Learn Kubernetes Basics / Explore Your App" %}

## Viewing Pods and Nodes

### Kubernetes Pods

* **pod:** a Kubernetes abstraction that represents one or more application containers \(e.g. Docker or rkt\) and some shared resources for those containers
  * hosts your application instance
* Resources include:
  * shared storage, as Volumes
  * networking, as a unique cluster IP address
  * information about how to run each container \(e.g. the container image version or specific ports to use\)



