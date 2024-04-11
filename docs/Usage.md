# [Ansible Provisioner](./README.md)

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

### Destroy the provisioned machines and create them again

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

[Back to the main page](./README.md)
