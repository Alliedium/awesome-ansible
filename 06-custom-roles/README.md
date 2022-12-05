# How to set up Arch and Manjaro machines

Please follow the steps from [Prerequisites](../README.md#prerequisites) prior to executing the commands below.


## Run playbook
=======
Besides, install all necessary requirements by executing the command:
>>>>>>> fde8f0c (some improvements)

```
ansible-galaxy install -r ./collections/requirements.yml
```

## General notes for creation of your own custom roles

1. In order to create a role run following command:
```
ansible-galaxy init <rolename>
```
Add task(s) into main.yml:
```
nano ./<rolename>/tasks/main.yml
```
In order to include the role in your playbook, use include_role module.

## Run playbook


