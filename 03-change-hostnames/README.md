# How to change hostnames via Ansible

## Prerequisites

Please follow the steps from [Prerequisites](../README.md#prerequisites) prior to executing the commands below.

## Run playbooks

1. Run the following playbook:
```
ansible-playbook -i ./inventory/hosts.yaml -v ./playbooks/change-hostnames_cidf.yml
```
2. Run another playbook, this time using stat module just for demonstration purposes, to rename the hosts as it was initially set up (you may name these hosts differently by changing values of respective variables in the inventory):
```
ansible-playbook -i ./inventory/hosts_initial.yaml -v ./playbooks/change-hostnames_stat.yml
```
