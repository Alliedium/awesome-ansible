## Practice --- How to ping hosts via playbook

1. Run the playbooks:
```
ansible -playbook -i ./inventory/ungrouped-hosts.yaml -v ./playbooks/ping.yml
```
```
ansible -playbook -i ./inventory/range-hosts.yaml -v ./playbooks/ping.yml
```
```
ansible -playbook -i ./inventory/grouped-hosts.yaml -v ./playbooks/ping.yml
```