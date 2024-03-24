# -*- mode: ruby -*-
# vi: set ft=ruby :
BOX="ubuntu/jammy64"
ANSIBLE="./provision.sh"
VAGRANT_PATH="/vagrant_data"
PROVISION_SCRIPT="https://raw.githubusercontent.com/lozaexequiel/provisioner/main/Ansible/provision.sh"
TEST_SCRIPT="https://raw.githubusercontent.com/lozaexequiel/provisioner/main/Ansible/testAnsibleConnection.sh"
TEST_SCRIPT_FILE="testAnsibleConnection.sh"
DEFAULT_CONF="https://raw.githubusercontent.com/lozaexequiel/provisioner/main/Ansible/example/.env.example"
CONF_FILE=".env.example"
CONF_DIR="example"
PROVIDER="virtualbox"
IP="192.168.0"
NETWORK="public_network"
INTERFACE="Realtek Gaming GbE Family Controller"
# Define ansible resources
ANSIBLE_MEMORY="8192"
ANSIBLE_CPU_COUNT="4"
# Define master resources
MASTER_COUNT=1
MASTER_MEMORY="8192"
MASTER_CPU_COUNT="4"
# Define node resources
NODE_COUNT=1
NODE_MEMORY="8192"
NODE_CPU_COUNT="4"
# Define Vagrant configuration
Vagrant.configure("2") do |config|
	config.vm.box = BOX
	if MASTER_COUNT < 1 and NODE_COUNT < 1 then
	  puts "MASTER_COUNT and NODE_COUNT must be greater than 0"
	  exit 1
	end
	boxes = []
	boxes << { :name => "ansible", :ip => "#{IP}.10", :cpus => ANSIBLE_CPU_COUNT, :memory => ANSIBLE_MEMORY, :network => NETWORK, :bridge => INTERFACE }	
	(1..MASTER_COUNT).each do |i|
		boxes << { :name => "master-#{i}", :ip => "#{IP}.#{i+10}", :cpus => MASTER_CPU_COUNT, :memory => MASTER_MEMORY, :network => NETWORK, :bridge => INTERFACE }
	      end
	      (1..NODE_COUNT).each do |i|
		boxes << { :name => "node-#{i}", :ip => "#{IP}.#{i+20}", :cpus => NODE_CPU_COUNT, :memory => NODE_MEMORY, :network => NETWORK, :bridge => INTERFACE }
	      end
	boxes.each_with_index do |opts, index|
		config.vm.define opts[:name] do |box|
			box.vm.synced_folder ".", VAGRANT_PATH
			box.vm.hostname = opts[:name]
			box.vm.network opts[:network], bridge: opts[:bridge], ip: opts[:ip]
			box.vm.provider PROVIDER do |vb|
				vb.cpus = opts[:cpus]
				vb.memory = opts[:memory]
			end
			box.vm.provision "shell", inline: <<-SHELL
			if [ ! -d #{VAGRANT_PATH}/#{CONF_DIR} ]; then
				mkdir -p #{VAGRANT_PATH}/#{CONF_DIR}
				curl -s #{DEFAULT_CONF} -o #{VAGRANT_PATH}/#{CONF_DIR}/#{CONF_FILE}
			fi

			if [ ! -f #{VAGRANT_PATH}/#{ANSIBLE} ]; then
				curl -s #{PROVISION_SCRIPT} -o #{VAGRANT_PATH}/#{ANSIBLE}
				chmod +x #{VAGRANT_PATH}/#{ANSIBLE}
			fi
			cd #{VAGRANT_PATH} && ./#{ANSIBLE}
		SHELL
		if index == boxes.length - 1 then
			box.vm.provision "shell", run: "always", inline: <<-SHELL
        	if [ ! -f #{VAGRANT_PATH}/#{TEST_SCRIPT_FILE} ]; then
			curl -s #{TEST_SCRIPT} -o #{VAGRANT_PATH}/#{TEST_SCRIPT_FILE}
			chmod +x #{VAGRANT_PATH}/#{TEST_SCRIPT_FILE}
		fi
		echo " INFO: You can now ssh into the ansible box with 'vagrant ssh ansible' "
		echo " INFO: You can check the ansible connection with 'vagrant ssh ansible -c 'cd #{VAGRANT_PATH} && ./#{TEST_SCRIPT_FILE}' "
		SHELL
		end
		end
	end
end