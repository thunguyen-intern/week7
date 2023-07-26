# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true

  config.vm.define "odoo1" do |odoo1|
    odoo1.vm.box = "ubuntu/focal64"
    odoo1.vm.network "private_network", ip: "192.168.56.10"
    odoo1.vm.synced_folder "./data", "/vagrant_data"
    odoo1.vm.provision "shell", path: "install.sh"
  end

  config.vm.define "odoo2" do |odoo2|
    odoo2.vm.box = "generic/debian10"
    odoo2.vm.network "private_network", ip: "192.168.56.11"
    odoo2.vm.synced_folder "./data", "/vagrant_data"
    odoo2.vm.provision "shell", path: "install.sh"
  end
  
end
