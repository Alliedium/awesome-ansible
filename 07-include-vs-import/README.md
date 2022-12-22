# How to set up Arch and Manjaro machines for users

Please follow the steps from [Prerequisites](../README.md#prerequisites) prior to executing the commands below and execute [`install-4server-all.yaml`](../06-custom-roles#run-playbook) playbook from [Example 6](../06-custom-role).

## Run playbooks

```
ansible-playbook -i ./inventory -v ./playbooks/sysadmin-users.yaml
ansible-playbook -i ./inventory -v ./playbooks/install-server-stuff-users.yaml
```
