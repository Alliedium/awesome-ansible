# How to install packages via Ansible

Please follow the steps from [Prerequisites](../README.md#prerequisites) prior to executing the commands below.

## Run playbooks

```
ansible-playbook -i ./inventory/hosts.yaml -v ./playbooks/update.yml
```
```
ansible-playbook -i ./inventory/hosts.yaml -v ./playbooks/qemu-guest-agent.yml
```
```
ansible-playbook -i ./inventory/hosts.yaml -v ./playbooks/qemu-guest-agent-package.yml
```