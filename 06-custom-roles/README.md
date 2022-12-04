## Practice --- How to set up manjaro machines


1. In order to create role run following command:
```
ansible-galaxy init <rolename>
```
Add task(s) into main.yml:
```
nano ./<rolename>/tasks/main.yml
```
In order to include the role in your playbook, use include_role module.