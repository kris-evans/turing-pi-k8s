# turing-pi-k8s


## ansible

List Nodes

```
ansible all -i ./inventory --list-hosts
```

Ping Nodes

```
ansible all -m ping -i ./inventory.yaml
```