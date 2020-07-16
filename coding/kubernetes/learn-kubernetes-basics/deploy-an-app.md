# Deploy an App

{% embed url="https://kubernetes.io/docs/tutorials/kubernetes-basics/create-cluster/" caption="Documentation / Tutorials / Learn Kubernetes Basics / Deploy an App" %}

## [Use kubectl to Create a Deployment](https://kubernetes.io/docs/tutorials/kubernetes-basics/deploy-app/deploy-intro/)

### Kubernetes Deployments

* you can deploy your containerized applications on top of a running k8s cluster
  * to do so, you create a Kubernetes **Deployment** configuration that instructs Kubernetes how to create and update instances of your application
* once you have a Deployment, the k8s master schedules application instances within the Deployment to run on individual Nodes in the cluster
* Kubernetes Deployment Controller continuously monitors application instances once the application instances are created
  * if the Node hosting an instance goes down or is deleted, the Deployment controller replaces the instance with an instance on another Node in the cluster
  * **this is a self-healing mechanism to address machine failure or maintenance**
    * fundamentally different approach to application management than installation scripts that would be used to start applications but did not allow recovery from machine failure



### Deploying your first app on Kubernetes

![](../../../.gitbook/assets/image%20%282%29.png)

* **Kubectl:** the Kubernetes command line interface
  * you can create and manage Deployments using Kubectl
* Kubectl uses the Kubernetes API to interact with the cluster

> Applications need to be packaged into one of the supported container formats in order to be deployed on Kubernetes

* when you create a Deployment, you'll need to specify:
  * the container image for your application
  * the number of replicas that you want to run
* you can change this information later by updating your Deployment



## Interactive Tutorial - Deploying an App

* a [Pod](https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/#understanding-pods) is the basic execution unit of a Kubernetes application
* each Pod is a part of a workload that is running on your cluster

### kubectl basics

* common format of a kubectl command is `kubectl {{ action }} {{ resource }}`
  * performs the action on the resource
  * you can use `--help` after the command to get additional info about possible parameters \(e.g. `kubectl get nodes -- help`\)

`kubectl version` - check that kubectl can talk to your cluster

```text
$ kubectl version
Client Version: version.Info{Major:"1", Minor:"17", GitVersion:"v1.17.3", GitCommit:"06ad960bfd03b39c8310aaf92d1e7c12ce618213", GitTreeState:"clean", BuildDate:"2020-02-11T18:14:22Z", GoVersion:"go1.13.6", Compiler:"gc", Platform:"linux/amd64"}
Server Version: version.Info{Major:"1", Minor:"17", GitVersion:"v1.17.3", GitCommit:"06ad960bfd03b39c8310aaf92d1e7c12ce618213", GitTreeState:"clean", BuildDate:"2020-02-11T18:07:13Z", GoVersion:"go1.13.6", Compiler:"gc", Platform:"linux/amd64"}
```

`kubectl get nodes` - view the nodes in the cluster

```text
$ kubectl get nodes
NAME       STATUS   ROLES    AGE     VERSION
minikube   Ready    master   3m43s   v1.17.3
```

* Kubernetes will choose where to deploy the app based on Node available resources

### Deploy our app

`kubectl create deployment` - deploy app

* you need to provide:
  * deployment name
  * app image location \(include the full repository url for images hosted outside Docker hub\)

```text
$ kubectl create deployment kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1
deployment.apps/kubernetes-bootcamp created
```

* creating this deployment did the following:
  * searched for a node where an instance of the application could be run
  * scheduled the application to run on that Node
  * configured the cluster to reschedule the instance on a new Node when needed

`get deployments` - list your deployments

```text
$ kubectl get deployments
NAME                  READY   UP-TO-DATE   AVAILABLE   AGE
kubernetes-bootcamp   1/1     1            1           2m46s
```

* there is 1 deployment running a single instance of your app
  * instance is running inside a Docker container on your node

### View our app

* pods within Kubernetes are running on a private, isolated network
  * visible by other pods and services by default if they are within the same kubernetes cluster
  * not visible by other pods and services outside the network
* kubectl allows us to interact through an API endpoint to communicate with our application
* the `kubectl` command creates a proxy that forwards communication into the cluster-wide, private network
* you can terminate the proxy by using `control + C` and it won't show any output while it is running



* open a second terminal window to run the proxy

`kubectl proxy`- run the proxy

```text
$ kubectl proxy
Starting to serve on 127.0.0.1:8001
```

* proxy acts as a connection between the host \(online terminal\) and the Kubernetes cluster
  * proxy allows direct access to the API from the terminals
* you can see all the APIs hosted through the proxy endpoint

`curl http://localhost:8001/version` - query the version directly through the api using the `curl` command

```text
$ curl http://localhost:8001/version
{
  "major": "1",
  "minor": "17",
  "gitVersion": "v1.17.3",
  "gitCommit": "06ad960bfd03b39c8310aaf92d1e7c12ce618213",
  "gitTreeState": "clean",
  "buildDate": "2020-02-11T18:07:13Z",
  "goVersion": "go1.13.6",
  "compiler": "gc",
  "platform": "linux/amd64"
}
```

* **if port 8001 is not accessible, ensure that the `kubectl proxy` is still running**
* the API server will automatically create an endpoint for each pod based on the pod name that is accessible through the proxy

`export POD_NAME=$(kubectl get pods -o go-template --template '') echo Name of the Pod: $POD_NAME`- get the name of the pod and store it in the `POD_NAME` environment variable

```text
$ export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}')
$ echo Name of the Pod: $POD_NAME
Name of the Pod: kubernetes-bootcamp-69fbc6f4cf-rss6f
```

* in order for the new deployment to be accessible without using the Proxy, a Service is required

\`\`

