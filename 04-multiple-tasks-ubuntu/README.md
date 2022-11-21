## Practice --- How to set up ubuntu machines

Prerequisites:

---------------------------------------------------------------------------
0. For this playbook we need bodsch.snapd role to be installed. 
We might install it using requirements.yml (which is more convenient if several roles are needed):

```
$ ansible-galaxy install -r requirements.yml
```

or just using role option of ansible-galaxy if we need just one role.
In case we need info about roles:
```
ansible-galaxy role --help
```
To install a new role:
```
ansible-galaxy role install bodsch.snapd
```
Should appear in the list:
```
ansible-galaxy role list
```

1. Then we run the playbook:
```
ansible-playbook -i ./inventory/hosts.yaml -v ./playbooks/prep-ubuntu4k3s.yml
```