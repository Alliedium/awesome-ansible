# awesome-ansible
## Practice --- How to automate machines setup via Ansible

# 1. Prerequisites

---------------------------------------------------------------------------
0. If you are going to use a Windows machine as config, you need to create a Linux VM on it, so you would be able to install ansible.
   You will need Windows Subsystem for Linux (WSL). Run Windows PowerShell as administrator:
```
wsl --install -d ubuntu
```
Then run the ubuntu shell.
1. Prepare config machine
* Copy ssh key onto it. To make this run the following command from the machine you have generated your key (same one you use on cloud-init VMs creation)
```
scp -i ~/.ssh/id_rsa_cloudinit ~/.ssh/id_rsa_cloudinit  <username>@<ip address>:~/.ssh/id_rsa_cloudinit
```
You might need to change permissions for the file:
```
chmod 400 ~/.ssh/id_rsa_cloudinit
```
or
```
chmod 600 ~/.ssh/id_rsa_cloudinit
```
2. Install ansible
```
sudo apt update
sudo apt upgrade
sudo apt install ansible
ansible --version
```
3. Create inventory
* In order to organize your ansible-related files create directory named ansible as below:
```
mkdir ansible
cd ./ansible
mkdir inventory
mkdir playbooks
cd ./inventory
mkdir cloud-init-vms
```
* Let's create hosts.yml file
```
nano ./hosts.yml
```
4. Let's see the list of hosts and their variables using the ansible-inventory command, which is used to display or dump the configured inventory as Ansible sees it:
```
ansible-inventory -i <path to hosts.yml> --list
```
5. Check connectivity with hosts:
```
ansible all -m ping -i inventory
```

# 2. Playbook examples

| Example | Details |
|------|-------|
| [Example 1](./01-ping-hosts) | ping.yml pings hosts and prints facts; contains multiple hosts examples: range, ungrouped, grouped |
| [Example 2](./02-install-a-single-package) | update.yml updates available packages using package manager depending on OS; qemu-guest-agent.yml installs qemu-guest-agent using apt module; qemu-guest-agent_package.yml installs qemu-guest-agent using package module |
| [Example 3](./03-change-hostnames) | change-hostnames_cidf.yml updates hostnames and edits cloud.cfg to preserve hostnames where necessary (detecting cloud-init image-generated VMs using cloud_init_data_facts); change-hostnames_stat.yml updates hostnames and edit cloud.cfg to preserve hostnames if such file exists (using stat for detection) |
| [Example 4](./04-multiple-tasks-ubuntu) | prep-ubuntu4k3s.yml configures ubuntu machines: installs and starts qemu-guest-agent, removes snap, updates NTP servers |
| [Example 5](./05-multiple-tasks-manjaro) | install_4server_all.yml configures manjaro and arch machines: removes snap, updates packages, installs git, yay, pacman-cli, enables AUR, installs pigz & pbzip2 | 


## References on: Ansible

1. [How to build your inventory](https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html)
2. [Ansible facts](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_vars_facts.html#ansible-facts)
3. [Variables](https://docs.ansible.com/ansible/2.5/user_guide/playbooks_variables.html)
4. [Return values](https://docs.ansible.com/ansible/latest/reference_appendices/common_return_values.html)
5. [Playbook debugger](https://docs.ansible.com/ansible/2.9/user_guide/playbooks_debugger.html)
6. [Debug module](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/debug_module.html)
7. [Ansible modules](https://docs.ansible.com/ansible/2.9/modules/list_of_all_modules.html)
8. [Roles](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html)
9. [Ansible Galaxy](https://galaxy.ansible.com/)
