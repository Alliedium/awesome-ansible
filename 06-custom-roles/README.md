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
In order to include the role in your playbook, use include_role module.

## Run playbook

In order to include the role in our playbook include_role module must be used. 
See the [example](./playbooks/install_4server_all.yml).

Then run the playbook:
```
ansible-playbook -i ./inventory -v ./playbooks/install_4server_all.yml -K
```