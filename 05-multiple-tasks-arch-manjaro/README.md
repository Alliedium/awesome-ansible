# How to set up Arch and Manjaro machines

Please follow the steps from [Prerequisites](../README.md#prerequisites) prior to executing the commands below.

## Run playbook

Run the playbook with -K or --ask-become-pass (we need this for the very first run until at least 1st task setting sudo users access with no password is completed):

```
ansible-playbook -i ./inventory -v ./playbooks/install-4server-all.yml -K
```
