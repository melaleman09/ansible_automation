~~~bash
.

## Install Ansible (Control Node)
## Install EPEL and Ansible Core:

sudo dnf install -y epel-release
sudo dnf install -y ansible-core


## Verify installation:
ansible --version

## Map IP Addresses to Hostnames (Control Node)
Edit the hosts file:
sudo vim /etc/hosts
Example:

192.168.12.x servera
192.168.12.x serverb

## Verify Network Connectivity
From the control node:

ping -c 4 servera
ping -c 4 serverb

## Repository Structure

root/ansible_automation/
├── ansible.cfg
├── inventory.example
├── playbooks/
│   ├── User_and_SSH_Setup.yml
│   └── useradd.yml
└── README.md

## SSH Installation and Configuration (Managed Hosts)
Check if SSH is installed
rpm -q openssh-server

## Install SSH if not present
sudo dnf install -y openssh-server

## Configure Firewall for SSH
Check current firewall settings:

sudo firewall-cmd --list-all

## Add SSH service if not present:

sudo firewall-cmd --add-service=ssh --permanent
sudo firewall-cmd --reload

## Verify SSH is allowed:

sudo firewall-cmd --list-all

## Enable and Start SSH
sudo systemctl enable --now sshd
sudo systemctl status sshd

## SSH Configuration
Edit the SSH configuration file:

sudo vim /etc/ssh/sshd_config
Example setting:

PermitRootLogin yes
⚠️ Allowing root login is not recommended in production environments.

## Restart SSH to apply changes:

sudo systemctl restart sshd

## Ansible Inventory Configuration
Edit the inventory file:

sudo vim /etc/ansible/hosts
Example:

[webservers]
servera
serverb
Hostnames are examples and should be replaced with real target systems.

## SSH Key Authentication
Generate SSH key on the control node
ssh-keygen

## Copy public key to managed hosts
ssh-copy-id servera
ssh-copy-id serverb

## Verify passwordless SSH access
ssh servera
ssh serverb

## Verify Ansible Connectivity
Test Ansible connectivity:

ansible webservers -m ping
Expected output:

ping: pong

## Playbooks
useradd.yml

This playbook ensures a Linux user account exists on all hosts in the webservers inventory group.
It creates the user and ensures a home directory exists.
Location:

/playbooks/useradd.yml
Run example:

ansible-playbook -i inventory.example playbooks/useradd.yml





