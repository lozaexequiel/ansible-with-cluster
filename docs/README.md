# Ansible Provisioner

This directory contains the configuration files for Ansible provisioner and is based on the main repository [Provisioner](https://github.com/lozaexequiel/provisioner).

## Table of Contents

- [Ansible Provisioner](#ansible-provisioner)
	- [Table of Contents](#table-of-contents)
	- [Prerequisites](#prerequisites)
	- [Usage](#usage)
	- [Project Structure](#project-structure)
	- [Variables](#variables)
		- [Global Variables](#global-variables)
		- [Ansible variables](#ansible-variables)
		- [Ansible playbooks](#ansible-playbooks)
	- [Ansible documentation](#ansible-documentation)

## Prerequisites

To use this project you need to have the following software installed:

- [Vagrant](https://www.vagrantup.com/)
- [VirtualBox](https://www.virtualbox.org/)

## [Usage](./Usage.md)

The usage of this project is documented in the [Usage](./Usage.md) section.

## [Project Structure](./Project-structure.md)

This project will create an environment directory and virtual machines with custom configuration.
To see the project structure go to [Project Structure](./Project-structure.md).

## Variables

### [Global Variables](https://github.com/lozaexequiel/provisioner/blob/main/README.md#global-variables)

Common variables for all provisioners are documented in the main repository.

### Ansible variables

The following variables are used by Ansible provisioner:

| Variable name | Description | Default value |
| --- | --- | --- |
| INVENTORY_FILE | Ansible inventory file | /vagrant_data/.env/.ansible/.inventory |
| ANSIBLE_DIR | Ansible directory | /home/vagrant |
| ANSIBLE_PLAYBOOK | Ansible playbook | /vagrant_data/ansible/PLAYBOOK/playbook.yml |
| ANSIBLE_PATH | Ansible path | /vagrant_data/.env/.ansible |
| ANSIBLE_CONFIG | Ansible configuration file | /vagrant_data/.env/.ansible/.ansible.cfg |
| PRIVATE_KEY_FILE | Private key file | /home/vagrant/.ssh/mykey |
| REMOTE_TMP | Remote temporary directory | /vagrant_data/.env/.ansible/.tmp/ansible-${USER} |
| BECOME_USER | Become user | root |
| ROLES_PATH | Roles path | /vagrant_data/.env/.ansible/.tmp/roles |
| ANSIBLE_VERSION | Ansible version | 2.9.6 |

You can change the values in the environment file.

### Ansible playbooks

The Ansible playbooks are located in the following directory:

```/vagrant_data/playbooks```

## Ansible documentation

The Ansible full documentation can be found in [Ansible website](https://docs.ansible.com/ansible/latest/index.html)

[Back to top](#ansible-provisioner)

[Go to main script repository](https://github.com/lozaexequiel/provisioner/tree/main/Ansible)
