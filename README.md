# 1. Prerequisites

All the examples that follow will assume that the environment described in this section is configured.

It is expected that a Proxmox cluster with a node having the name `px-node-I` is set up.

(**NOTE:** if named differently should be edited in the `.env.*` files mentioned below).

It is also assumed that `vnet` was created in `SDN VLAN 3` zone on linux bridge `vmbr0`, its name is `v3`.

(**NOTE:** LAN 3 should be set up in `OPNsense` according to the instruction provided at [lesson 29](https://github.com/Alliedium/devops-course-2022/tree/main/29_configuring_opnsense_and_creating_vms_via_scripts_and_manual_10_nov_2022)).

There are at least 2 ways to create necessary VMs for the environment: a) automatic and b) manual

## Fully-automatic environment creation (Ubuntu as well as Arch instead of Manjaro)

### Preliminary actions

* Get cloud-init scripts on the Proxmox node mentioned above:
```
apt install git
git clone https://github.com/Alliedium/awesome-linux-config.git
```
If you already have the repository, make sure your version is the latest one:
```
cd ./awesome-linux-config
git pull
```
* SSH key must be placed here: /root/.ssh/id_rsa_cloudinit.pub

* Create resource pool:
  ```
  pvesh create /pools --poolid ansible-pool
  ```
* Go to the git directory you've cloned from git:
```
cd ./awesome-linux-config/proxmox7/cloud-init/
```

### Creating config VM

If you are going to use a Windows machine as config, you need to create a Linux VM on it, so you would be able to install `Ansible`.
   You will need Windows Subsystem for Linux (WSL). Run Windows PowerShell as administrator:
```
wsl --install -d ubuntu
```
Then run the ubuntu shell. 

Otherwise, if you are going to create a separate VM in Proxmox as a config machine, please follow the following steps:

* Copy & edit (if necessary) [.env.control](./cloud-init/.env.control) (from this repository!)
* Apply env:
```
set -a; source ./.env.control; set +a
```
* Run image download:
```
./download-cloud-init-images.sh
```
* Run image customization:
```
./customize-cloud-init-images.sh
```
* Create ubuntu template:
```
./create-template.sh
```
* Create control node:
```
./create-vms.sh
```

### Creating VMs through Cloud Init scripts

Other steps are to be done both for the cases when WSL is used and when a separate config VM in Proxmox was created.

* Copy & edit (if necessary) [.env.ubuntu](./cloud-init/.env.ubuntu) (from this repository!)
* Apply env:
```
set -a; source ./.env.ubuntu; set +a
```
* Create 3 ubuntu nodes:
```
./create-vms.sh
```
* Copy & edit (if necessary) [.env.arch](./cloud-init/.env.arch) (from this repository!)
* Apply env:
```
set -a; source ./.env.arch; set +a
```
* Run image download:
```
./download-cloud-init-images.sh
```
* Create arch template:
```
./create-template.sh
```
* Create 2 arch nodes:
```
./create-vms.sh
```

## Manual VM creation (Manjaro)

Follow the Manjaro installation steps from [lesson 22](https://github.com/Alliedium/devops-course-2022/blob/main/22_networks_vlan_opnsense_vms_25-oct-2022/practice.md)

Necessary VM parameters: Disk size = 20 GiB, RAM = 3072 MiB (3 GiB) RAM size

**NOTE:** Before converting the VM to template, you will need to copy ssh public key from the Proxmox node shell.
In order to be able to make it, first enable sshd:
```
sudo systemctl enable sshd --now
```
Then edit `sshd_config` file on your Manjaro VM:
```
sudo nano /etc/ssh/sshd_config 
```
Make sure following parameters are not commented:
```
Port 22
PubkeyAuthentication yes
PasswordAuthentication yes
```
In the case you had made any changes run:
```
sudo systemctl restart sshd
```
Then establish the connection from the node via ssh (you will be asked to enter password):
```
ssh <manjaro-user>@<manjaro-ip>
```
Then run `ssh-copy-id` as following (you will be asked to enter password):
```
ssh-copy-id -i ~/.ssh/id_rsa_cloudinit.pub <manjaro-user>@<manjaro-ip>
```
Now you are ready to convert the machine to template.
Further, please create a linked clone basing on this template, connect it to VLAN 3 and set a static IP address via `nmtui` tool.
According to the hosts.yml, the address is 10.3.1.41/24, gateway and DNS server are set to 10.3.1.1.
In case your manjaro's address is different, make sure you change it within the inventory.

## Setting up config machine

1. Prepare config machine
* Copy _private_ ssh key onto it. To make this run the following command from the machine you have generated your key (same one you use on cloud-init VMs creation)
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
2. Install `Ansible`
```
sudo apt update
sudo apt upgrade
sudo apt install ansible
ansible --version
```

# 2. General notes on creating your own custom inventory and playbooks

* In order to organize your Ansible-related files create directory named `ansible` as below:
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
* Let's see the list of hosts and their variables using the `ansible-inventory` command, which is used to display or dump the configured inventory as `Ansible` sees it:
```
ansible-inventory -i <path to hosts.yml> --list
```
* Check connectivity with hosts:
```
ansible all -m ping -i inventory
```

# 3. Playbook examples

| Example | Details |
|------|-------|
| [Example 1](./01-ping-hosts) | ping.yml pings hosts and prints facts; contains multiple hosts examples: range, ungrouped, grouped |
| [Example 2](./02-install-a-single-package) | update.yml updates available packages using package manager depending on OS; qemu-guest-agent.yml installs qemu-guest-agent using apt module; qemu-guest-agent_package.yml installs qemu-guest-agent using package module |
| [Example 3](./03-change-hostnames) | change-hostnames_cidf.yml updates hostnames and edits cloud.cfg to preserve hostnames where necessary (detecting cloud-init image-generated VMs using cloud_init_data_facts); change-hostnames_stat.yml updates hostnames and edit cloud.cfg to preserve hostnames if such file exists (using stat for detection) |
| [Example 4](./04-multiple-tasks-ubuntu) | prep-ubuntu4k3s.yml configures ubuntu machines: installs and starts qemu-guest-agent, removes snap, updates NTP servers |
| [Example 5](./05-multiple-tasks-arch-manjaro) | install_4server_all.yml configures manjaro and arch machines: removes snap, updates packages, installs git, yay, pacman-cli, enables AUR, installs pigz & pbzip2 | 
| [Example 6](./06-custom-roles-arch-manjaro) | install_4server_all.yml configures manjaro and arch machines using custom roles | 
