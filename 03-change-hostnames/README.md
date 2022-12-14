# How to change hostnames via Ansible

## Prerequisites

Please follow the steps from [Prerequisites](../README.md#prerequisites) prior to executing the commands below.

## Run playbooks

1. Run the following playbook using cloud_init_data_facts module:
```
ansible-playbook -i ./inventory/hosts.yaml -v ./playbooks/change-hostnames-to-simple-cidf.yml -K
```
2. Run another playbook, this time using stat module just for demonstration purposes, to rename the hosts as it was initially set up (you may name these hosts differently by changing values of respective variables in the inventory):
```
ansible-playbook -i ./inventory/hosts_initial.yaml -v ./playbooks/change-hostnames-to-simple-stat.yml -K
```
3. Run any playbook, this time using another hosts file, which does not include any variables. Instead, group_vars and host_vars are used to specify all the parameters which may differ on the group or host level.
Kindly note, that the group_vars and host_vars directories should be placed in ./inventory directory. They include .yml files named exactly as group they apply to, or ip address of a particular host.
```
ansible-playbook -i ./inventory/hosts_no_vars.yaml -v ./playbooks/change-hostnames-to-compose-stat.yml -K
```
Same command would work with cloud_init_data_facts module:
```
ansible-playbook -i ./inventory/hosts_no_vars.yaml -v ./playbooks/change-hostnames-to-compose-cidf.yml -K
```
4. You might run any of these without specifying the exact host file:
```
ansible-playbook -i ./inventory ./playbooks/change-hostnames-to-compose-stat.yml -K
```