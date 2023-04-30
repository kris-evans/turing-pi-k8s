# TuringPi K8S Ansible

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
ansible-playbook -i ./inventory.yaml ./roles/cluster-node.yaml
```

4. Apply kubernetes control role

This role conifugres Kubernetes control nodes and enables support for Helm and Arkade.

```
ansible-playbook -i ./inventory.yaml ./roles/kubernetes-control.yaml
```

5. Apply kubernetes agent role

This role configures the Kubernetes agent nodes and connects them to the K3S cluster.

```
ansible-playbook -i ./inventory.yaml ./roles/kubernetes-agent.yaml
```

6. Apply kubernetes networking role

This role configures metallb in the K3S cluster so you can allocate IP Address to services using a load balancer.

```
ansible-playbook -i ./inventory.yaml ./roles/kubernetes-network.yaml
```