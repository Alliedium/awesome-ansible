## Practice --- How to change hostnames via Ansible

Prerequisites:

---------------------------------------------------------------------------
0. For this playbook we need new hostnames to be specified.
Make sure you have this parameter specified for each of your hosts.

1. Then we run the playbook:
```
ansible-playbook -i ./inventory/hosts.yaml -v ./playbooks/change-hostnames_cidf.yml
```
2. Run another playbook, this time using stat module just for demonstration purpose, to rename the hosts as it was initially set up (you might have named them differently though):
```
ansible-playbook -i ./inventory/hosts_initial.yaml -v ./playbooks/change-hostnames_stat.yml
```
