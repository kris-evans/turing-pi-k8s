# TuringPi K8S Ansible

## Prerequisites

* Python3

## Getting Started

1. Clone the repo 

2. Activate the venv

```
source ./bin/activate
```

## Ansible Commands

### List Nodes

```
ansible all -i ./inventory --list-hosts
```

### Ping Nodes

```
ansible all -m ping -i ./inventory.yaml
```