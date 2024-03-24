# Ansible Provisioner

This directory contains the configuration files for Ansible provisioner and is based on the main repository [Provisioner](https://github.com/lozaexequiel/provisioner).

## Table of Contents

- [Ansible Provisioner](#ansible-provisioner)
	- [Table of Contents](#table-of-contents)
	- [Prerequisites](#prerequisites)
	- [Usage](#usage)
		- [Clone the repository](#clone-the-repository)
		- [Change to the directory](#change-to-the-directory)
		- [Start the provisioner](#start-the-provisioner)
		- [Provision custom machines](#provision-custom-machines)
		- [Stop the provisioned machines](#stop-the-provisioned-machines)
		- [Destroy the provisioned machines](#destroy-the-provisioned-machines)
		- [Test the provisioner](#test-the-provisioner)
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

## Usage

### Clone the repository

To use this provisioner you need to clone the repository:

~~~bash
git clone https://github.com/lozaexequiel/ansible-with-cluster
~~~

### Change to the directory

Change to the directory of the provisioner:

~~~bash
cd ansible-with-cluster
~~~

### Start the provisioner

To use this provisioner you need to run the following command:

~~~bash
vagrant up
~~~

### Provision custom machines

After you provision the machines you can use the following command to run the provisioner again with the new configuration:

~~~bash
vagrant provision
~~~

If you want to run the provisioner again resetting the configuration you can use the following command:

```vagrant up --provision``` or ```vagrant reload --provision```

If the custom configuration is not working you can delete the machine and create it again with the new configuration using the following command

~~~bash
vagrant destroy -f && vagrant up
~~~

This command will delete all the data in the virtual machine not the configuration files or data in the host machine and create the machine again with the new configuration.

### Stop the provisioned machines

To stop the machines you can use the following command:

~~~bash
vagrant halt
~~~

### Destroy the provisioned machines

To destroy the provisioner you can use the following command:

~~~bash
vagrant destroy -f
~~~

Please note that this command will delete all the data in the virtual machine not the configuration files or data in the host machine.

### Test the provisioner

To test the provisioner you can use the following command:

~~~bash
vagrant ssh ansible -c "./vagrant_data/testAnsibleConnection.sh"
~~~

This command will test the connection to the provisioned machines and will show after all the machines were provisioned to execute manually the Ansible command.

Example output:

~~~bash
INFO: You has successfully provisioned 3 servers
node-1 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
master-1 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}

~~~

## Project Structure

This project will create the following directory structure:

~~~bash
./vagrant_data
├── /.env # Environment directory
├── ├── /.env # Environment file
├── ├── /.ansible # Ansible directory
├── ├── ├── /.ansible.cfg # Ansible configuration file
├── ├── ├── /.inventory # Ansible inventory file
├── ├── ├── /.tmp # Temporary directory
├── ├── ├── ├── /ansible-${USER} # Remote temporary
├── ├── ├── ├── /roles # Roles directory
~~~

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
