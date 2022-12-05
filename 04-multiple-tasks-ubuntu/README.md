# How to set up Ubuntu machines

## Prerequisites

Please follow the steps from [Prerequisites](../README.md#prerequisites) prior to executing the commands below.

Also for this playbook we need `bodsch.snapd` role to be installed.
We might install it using requirements.yml (which is more convenient if several roles are needed):

```
ansible-galaxy install -r requirements.yml
```

or just using role option of `ansible-galaxy` if we need just one role.

In case we need info about roles:
```
ansible-galaxy role --help
```
To install a new role:
```
ansible-galaxy install bodsch.snapd
```
Should appear in the list:
```
ansible-galaxy list
```

## Run playbook

```
ansible-playbook -i ./inventory/hosts.yaml -v ./playbooks/prep-ubuntu4k3s.yml
```
