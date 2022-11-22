## Practice --- How to change hostnames via Ansible

Prerequisites:

---------------------------------------------------------------------------
0. For this playbook we need new hostnames to be specified.
Make sure you have this parameter specified for each of your hosts.

1. Then we run the playbook:
```
ansible-playbook -i ./inventory/hosts.yaml -v ./playbooks/change-hostnames.yml
```
