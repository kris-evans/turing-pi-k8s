# TuringPi K8S Ansible

This set of Ansible playbooks implements [the guide at turingpi.com](https://help.turingpi.com/hc/en-us/articles/8942873470877-The-plan) to setup a K3S cluster on top of a Turing Pi 2 cluster. 

## Prerequisites

* Python3

## Getting Started

1. Clone the repo 

2. Activate the venv

```
source ./bin/activate
```

## New Cluster Setup

1. List all nodes

```
ansible all -i ./inventory --list-hosts
```

2. Ping nodes

```
ansible all -m ping -i ./inventory.yaml
```

3. Apply cluster node role

This role properly sets up nodes in the cluster so they can talk to each other. 

```
ansible-playbook -i ./inventory.yaml ./roles/01-cluster-node.yaml
```

4. Apply storage node role

This role configures the ssd to be mounted at /data.

```
ansible-playbook -i ./inventory.yaml ./roles/02-storage-node.yaml
```

5. Apply kubernetes control role

This role conifugres Kubernetes control nodes and enables support for Helm and Arkade.

```
ansible-playbook -i ./inventory.yaml ./roles/03-kubernetes-control.yaml
```

6. Apply kubernetes agent role

This role configures the Kubernetes agent nodes and connects them to the K3S cluster.

```
ansible-playbook -i ./inventory.yaml ./roles/04-kubernetes-agent.yaml
```

7. Apply kubernetes networking role

This role configures metallb in the K3S cluster so you can allocate IP Address to services using a load balancer.

```
ansible-playbook -i ./inventory.yaml ./roles/05-kubernetes-network.yaml
```

7. Apply kubernetes cd role

Configures ArgoCD in the cluster and exposes it on a predefined LB port. 

```
ansible-playbook -i ./inventory.yaml ./roles/07-kubernetes-cd.yaml
```