# kubernetest_learning
A repository of manifests created while learning Kubernetes

KIND setup
Kubernetes inside Docker (KIND) is a quck and easy way to setup a kubernetes cluster using Docker.

Pre-requisites:
A linux installation (Centos/RedHat/OEL/Ubuntu) with docker and kubectl installed.

Steps to setup KIND:

1) Download the binary

curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.14.0/kind-linux-amd64

2) Make it executable and move it to /usr/local/bin

chmod +x ./kind
mv ./kind /usr/local/bin/kind

3) Create the KIND cluster configuration file
The config file show below creates a cluster with one master node and two worker nodes.

cat kind-example-config.yaml
#three node (two workers) cluster config
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: worker
- role: worker

4) Create the cluster
Execute the following command to create the cluster.

kind create cluster --config kind-example-config.yaml

5) 
