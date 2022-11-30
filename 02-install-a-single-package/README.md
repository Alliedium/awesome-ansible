## Practice --- How to install packages via Ansible

1. Run the playbooks:
```
ansible-playbook -i ./inventory/hosts.yaml -v ./playbooks/update.yml
```
```
ansible-playbook -i ./inventory/hosts.yaml -v ./playbooks/qemu-guest-agent.yml
```
```
ansible-playbook -i ./inventory/hosts.yaml -v ./playbooks/qemu-guest-agent_package.yml
```