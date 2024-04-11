# Ansible Provisioner

## Project Structure

The project structure is based on the following diagram:

![Project Structure](./images/ansible-architecture.svg)

This project will create the following directory structure with the scripts and configuration files:

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

[Back to top](#ansible-provisioner)

[Go to main repository](README.md)
