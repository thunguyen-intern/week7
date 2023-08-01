# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true

  config.vm.define "odoo1" do |odoo1|
    odoo1.vm.box = "ubuntu/focal64"
    odoo1.vm.network "private_network", ip: "192.168.56.10"
    odoo1.vm.synced_folder ".", "/vagrant_data"
    odoo1.vm.provision "shell", inline: <<-SHELL
    	sudo apt-get update
    	sudo apt-get install -y nginx
  SHELL
  end 
  {"vm1" => "192.168.56.11", "vm2" => "192.168.56.12", "vm3" => "192.168.56.13"}.each do |vm_name, vm_ip|
    config.vm.define vm_name do |vm_config|
      vm_config.vm.box = "ubuntu/focal64"
      vm_config.vm.network "private_network", ip: vm_ip
      vm_config.vm.provision "shell", inline: <<-SHELL
        # Install Docker
        curl -fsSL https://get.docker.com -o get-docker.sh
        sh get-docker.sh

        # Enable remote Docker access (replace with secure setup in production)
        echo 'DOCKER_OPTS="-H tcp://0.0.0.0:2375 -H unix:///var/run/docker.sock"' >> /etc/default/docker
        systemctl restart docker
      SHELL
    end
  end

end
