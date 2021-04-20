[![published](https://static.production.devnetcloud.com/codeexchange/assets/images/devnet-published.svg)](https://developer.cisco.com/codeexchange/github/repo/mohitmksgit/ansible_cisco_info)

# Cisco informational playbooks

## Introduction

This repository contains various ansible playbooks that could be used to gather information from Cisco IOS & NXOS devices.

## High level steps

1. Clone code from Gitlab
2. Add admin credentials in group variable file
3. Secure admin credentials using ansible vault
4. Running ansible playbook

## Prerequisite 

Ansible version <2.9.10


## 1. Repository clone instructions

Clone with SSH

git clone git@github.com:mohitmksgit/cisco_info.git

Clone with HTTPS

git clone https://github.com/mohitmksgit/cisco_info.git

## 2. Add credentials in group variable file

Cisco device group variables are stored in "group_vars" folder as "cisco_ios.yml" & "nxos.yml". 

| File                | Description                                                                 |
| --------------------| ----------------------------------------------------------------------------|
| cisco_ios.yml       | Stores credentials & other variables for Cisco IOS devices                                 |
| nxos.yml            | Stores credentials & other variables for Cisco NXOS devices  

### 2.1 Navigate to repository clone folder:
cd cisco_info

### 2.2 Add your admin credentials into "cisco_ios" group variable file:

nano group_vars/cisco_ios.yml

ansible_ssh_user: (user.admin)

ansible_ssh_pass: (admin password)

auth_pass: (admin password)

### 2.3 Add your admin credentials into "nxos" group variable file:

nano group_vars/nxos.yml

ansible_ssh_user: (user.admin)

ansible_ssh_pass: (admin password)

auth_pass: (admin password)

## 3. Secure admin credentials using ansible vault

You must use the ansible-vault encryption to secure your admin credentials. Enter command mentioned below & provide a password to secure ansible vault. You will be required to enter this vault password while running a playbook.

ansible-vault encrypt cisco_ios.yml nxos.yml

## 4. Running ansible playbook
Use ansible-playbook command to run a playbook. You must add "--ask-vault-pass" keyword so that you are prompted to enter ansible-vault credentials.

ansible-playbook -i ntw.devices.host PLAYBOOK_NAME.yml --ask-vault-pass

## 5. Targeting specific hosts and groups while running a playbook

When you execute Ansible by running a playbook, you must choose which managed nodes or groups you want to execute against. Patterns let you run commands and playbooks against specific hosts and/or groups in your inventory. An Ansible pattern can refer to a single host, an IP address, an inventory group, a set of groups, or all hosts in your inventory.

### 5.1 Limit to one host

ansible-playbook -i ntw.devices.host PLAYBOOK_NAME.yml --ask-vault-pass--limit "host1"

### 5.2 Limit to multiple hosts

ansible-playbook -i ntw.devices.host PLAYBOOK_NAME.yml --limit "host1,host2"

### 5.3 Exclude host/group (Negated limit) from playbook execution
 
NOTE: Single quotes MUST be used to prevent bash interpolation.

ansible-playbook -i ntw.devices.host PLAYBOOK_NAME.yml --limit 'all:!host1'

### 5.4 Limit to host group

ansible-playbook -i ntw.devices.host PLAYBOOK_NAME.yml --limit 'group1'

## 6. Inventory file 

Inventory is stored in "hosts" file. Please modify hostname & IP addresses according to your lab. 

## 7. Playbook description
| Playbook file                          | Description                                                                 |
| ---------------------------------------| ----------------------------------------------------------------------------|
| cisco_show_ver_ios.yml                 | Runs "show version" command on IOS device                                                     |
| cisco_show_ver_nxos.yml                | Runs "show version" command on NXOS device  
| cisco_show_acl_ios.yml                 | Shows a list of Access-lists (ACL) configured on Cisco IOS device 
| cisco_show_acl_nxos.yml                | Shows a list of Access-lists (ACL) configured on Cisco NXOS device   
| cisco_show_cpu_ios.yml                 | Shows CPU usage on Cisco IOS device 
| cisco_show_cpu_nxos.yml                | Shows CPU usage on Cisco NXOS device                                                 
| cisco_show_inv_ios.yml                 | Runs "show inventory" command on IOS device                                               |
| cisco_show_inv_nxos.yml                | Runs "show inventory" command on NXOS device                   |
| cisco_show_ntp_status_ios.yml          | Shows NTP sync status on IOS device                                          |
| cisco_show_ntp_status_nxos.yml         | Shows NTP sync status on NXOS device                                            |
| cisco_backup_config_ios.yml            | Saves running configuration to playbook directory for IOS device          |
| cisco_backup_config_nxos.yml           | Saves running configuration to playbook directory for NXOS device          |
| cisco_facts_ios_brief.yml              | Shows basic info like Serial number,Model,OS version for IOS device |
| cisco_facts_nxos_brief.yml             | Shows basic info like Serial number,Model,OS version for NXOS device |                                        
| cisco_os_update_verification_ios.yml   | Useful in IOS upgrade task. Playbook runs ping test to defined IP`s, takes backup of running config & Checks CPU, Memory & disk space usage
| cisco_ansible_inv_vs_hostname_ios.yml  | Compares IOS device hostname with ansible inventory host_alias         |
| cisco_ansible_inv_vs_hostname_nxos.yml | Compares NXOS device hostname with ansible inventory host_alias

## 8. Additional information about Ansible vault

### 8.1 Edit ansible vault file
   
ansible-vault edit "filename"

### 8.2 Viewing encrypted vault file
   
ansible-vault view "filename"

## 9. Updating a local repository with latest changes from a Git repository

git pull is a Git command used to update the local version of a repository from a remote (Gitlab). For example, if the branch you have checked out tracks origin/master, git pull is equivalent to git pull origin master.

Run this command to download latest version of repository on your local machine:

git pull

## 10. Reference

Here is the list of Ansible modules used in this repository:

ios_ping – Tests reachability using ping from Cisco IOS network devices
https://docs.ansible.com/ansible/2.9/modules/ios_ping_module.html#ios-ping-module

ios_facts – Collect facts from remote devices running Cisco IOS 
https://docs.ansible.com/ansible/2.9/modules/ios_facts_module.html#ios-facts-module

ios_command – Run commands on remote devices running Cisco IOS 
https://docs.ansible.com/ansible/2.9/modules/ios_command_module.html#ios-command-module

nxos_ping – Tests reachability using ping from Nexus switch 
https://docs.ansible.com/ansible/2.9/modules/nxos_ping_module.html#nxos-ping-module

nxos_facts – Gets facts about NX-OS switches 
https://docs.ansible.com/ansible/2.9/modules/nxos_facts_module.html#nxos-facts-module

nxos_command – Run arbitrary command on Cisco NXOS devices 
https://docs.ansible.com/ansible/2.9/modules/nxos_command_module.html#nxos-command-module

## 11. Roadmap

More useful informational playbooks will be added into this repository

## 12. Known issues
None

