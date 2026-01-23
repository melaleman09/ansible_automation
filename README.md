# ansible_automation
This repository documents the installation and initial configuration of an
Ansible control node on a RHEL-based system. It includes installing required
packages, verifying connectivity, configuring SSH, and creating an Ansible
inventory.
## Requirements

## Repository Structure
---
ansible_automation
  |-inventory.example
  |-ansible.cfg
  |-playbooks
      |-user_and_SSH_setup.yml

## Install
ansible-core and epel-release
verify:
rpm -q epel-release
ansible --version

## SSH Configuration file
vim /etc/ssh/sshd_config 
PermitRootLogin yes

## Add SSH service to firewall
firewall-cmd --add-service=ssh --perm

## Confirm ssh service active and enabled
systemctl status sshd
systemctl enable --now sshd
systemctl restart sshd
systemctl status sshd

## Ansible Inventory
vim /etc/ansible/hosts
[webservers]
servera 
serverb

## Map IP Addresses to host names
192.168.12.x servera
192.168.12.x serverb

ssh-keygen fron controlnode, generate a public key
ssh-copy-id servera type yes and enter for passphrase and enter again
ssh-copy-id serverb type yes and enter for passphrase and enter again

ssh servera to test without need for password
ssh serverb to test without need for password

## Check Connectivity
Verify with Ansible Ping
ansible all -m ping
Expected output:
ping: pong






