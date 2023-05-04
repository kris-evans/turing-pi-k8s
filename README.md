# TuringPi K8S Ansible

This set of Ansible playbooks implements [the guide at turingpi.com](https://help.turingpi.com/hc/en-us/articles/8942873470877-The-plan) to setup a K3S cluster on top of a Turing Pi 2 cluster. 

## Cluster URLs ##
* [Traeffik](http://192.168.1.170/)
* [ArgoCD](http://192.168.1.171)
* [AlertManager](http://192.168.1.172:9093)
* [Prometheus](http:192.168.1.173:9090)
* [Grafana](http:192.168.1.174)

## Getting Started

### Prerequisites

* Python3
* Ansible

### Developng

1. Clone the repo 

2. cd /path/to/repo

3. Create a venv

```
python -m venv /path/to/project/venv
```

4. Activate the venv

```
source /path/to/project/venv/bin/activate
```

5. Install venv dependencies

```
/path/to/project/venv/bin/pip install -r ./requirements.txt
```

### Commands

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

8. Apply kubernetes cd role

Configures ArgoCD in the cluster and exposes it on a predefined LB port. 

```
ansible-playbook -i ./inventory.yaml ./roles/07-kubernetes-cd.yaml
```

9. Apply kubernetes monitoring role

Configures Prometheus, Grafana, and AlertManager.

```
ansible-playbook -i ./inventory.yaml ./roles/08-kubernetes-monitoring.yaml
```