# kubernetest_learning
A repository of manifests created while learning Kubernetes

### KIND setup
Kubernetes inside Docker (KIND) is a quck and easy way to setup a kubernetes cluster using Docker.

Pre-requisites:
A linux installation (Centos/RedHat/OEL/Ubuntu) with docker and kubectl installed.

Steps to setup KIND:

1) Download the binary
```
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.14.0/kind-linux-amd64
```
2) Make it executable and move it to /usr/local/bin
```
chmod +x ./kind
mv ./kind /usr/local/bin/kind
```
3) Create the KIND cluster configuration file

The config file show below creates a cluster with one master node and two worker nodes.
```
cat kind-example-config.yaml
#three node (two workers) cluster config
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: worker
- role: worker
```

4) Create the cluster
Execute the following command to create the cluster.
```
kind create cluster --config kind-example-config.yaml --name test-cluster
```

5) Verify cluster is up.
To verify that our cluster is up and running, we could run the **kind get clusters** command.

6) Using kubectl to interact with the cluster
We could now set the context in our kubectl command so that we interact with our cluster.
```
kubectl config set-context kind-test-cluster
```

##### Note:
Apparently, the kind setup did not work on a Centos 7 node with Docker installed. To get it to work, I first had to provision an Ubuntu 20.04 system, setup minikube on it using the script avaialbe in this repo.

## Generating YAML manifests

We do not need to memorize the different components that go into the creation of YAML manifests for most deployment types. We could just create YAML files using the kubectl command, modify them as per our requirement and then apply them via kubectl.

In the below example, we create a manifest file for deploying a single pod:

```
kubectl run  nginx-pod --image=nginx --dry-run=client -o yaml >> ngingx-pod.yaml
```
To create the pod, we simply need to apply the manifest.
```
kubectl apply -f ngingx-pod.yaml
```
