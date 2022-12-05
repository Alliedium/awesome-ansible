# How to ping hosts via playbook

Please follow the steps from [Prerequisites](../README.md#prerequisites) prior to executing the commands below.

## Run playbooks

```
ansible-playbook -i ./inventory/ungrouped-hosts.yaml -v ./playbooks/ping.yml
```
```
ansible-playbook -i ./inventory/range-hosts.yaml -v ./playbooks/ping.yml
```
```
ansible-playbook -i ./inventory/grouped-hosts.yaml -v ./playbooks/ping.yml
```
