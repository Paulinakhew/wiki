---
description: This has notes that I've created from the Kubernetes Basics documetation.
---

# Learn Kubernetes Basics

## What can Kubernetes do?

* you can enable applications to be released and updated quickly through containerization
  * meet users' needs by deploying updates to your web services several times a day
* Kubernetes helps you make sure containerized applications run when and where you want and helps them find the resources and tools they need to work
* **Kubernetes:** a production-ready, open source platform
  * designed with Google's experience in container orchestration + ideas from the community



## Create a Cluster

### Using Minikube to Create a Cluster

* **Kubernetes cluster:** a highly available cluster of computers that are connected to work as a single unit
* you can deploy an application to a cluster without tying them to a specific machine
* **containerizing** applications makes sure that they are packaged in a way that decouples them from individual hosts
  * containerized apps are more flexible and available than apps that are installed directly onto specific machines
* **Kubernetes automates the distribution and scheduling of application containers across a cluster in a more efficient way**
* a Kubernetes cluster consists of two types of resources:
  * the **Master** coordinates the cluster
  * **Nodes** are the workers that run applications



![Cluster diagram](../../.gitbook/assets/image.png)

* **The master manages the cluster by coordinating all activities**
  * schedules applications
  * maintaining applications' desired state
  * scales applications
  * rolls out new updates





