# How to set up Arch and Manjaro machines

Please follow the steps from [Prerequisites](../README.md#prerequisites) prior to executing the commands below.

Besides, install all necessary requirements by executing the command:
```
ansible-galaxy install -r ./collections/requirements.yml
```

## General notes for creation of your own custom roles

In order to create a role run following command:
```
ansible-galaxy init <rolename>
```
Add task(s) into main.yml:
```
nano ./<rolename>/tasks/main.yml
```
In order to include the role in your playbook, use [one of the ways provided by Ansible](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html#using-roles). See the [example](./playbooks/install-4server-all.yml).

## Run playbook

Then run the playbook with `-K` or `--ask-become-pass` (we need this for the very first run until at least 1st task setting sudo users access with no password is completed):
```
ansible-playbook -i ./inventory -v ./playbooks/install-4server-all.yml -K
```

It is also possible to run preliminary only `preinstall` tag with `-K` or `--ask-become-pass` by
```
ansible-playbook -i ./inventory -v ./playbooks/install-4server-all.yml --tags preinstall -K
```
and after this run the whole playbook without any additional options by
```
ansible-playbook -i ./inventory -v ./playbooks/install-4server-all.yml
```