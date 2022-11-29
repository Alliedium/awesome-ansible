# awesome-ansible
## Practice --- How to automate machines setup via Ansible

Prerequisites:

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