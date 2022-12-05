# How to set up Arch and Manjaro machines

Please follow the steps from [Prerequisites](../README.md#prerequisites) prior to executing the commands below.

Kindly note that in order to run the playbooks from this section you need significantly more disk space than for the previous examples.

Our manjaro's disk size is set to 20 GiB and 6144 MiB (6 GiB) RAM size.

Arch machines' disk size is set to 20 GiB as well, but can use a little less RAM due to UI absence: 4096 MiB (4 GiB). 

## Run playbook

1. In order to create role run following command:
```
ansible-galaxy init <rolename>
```
Add task(s) into main.yml:
```
nano ./<rolename>/tasks/main.yml
```
In order to include the role in your playbook, use include_role module.