## Practice --- How to install packages via Ansible

1. Run the playbooks:
```
ansible-playbook -i ./inventory/hosts.yaml -v ./playbooks/apt.yml
```
```
ansible-playbook -i ./inventory/hosts.yaml -v ./playbooks/qemu-guest-agent.yml
```
