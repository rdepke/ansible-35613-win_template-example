# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define :ansible, primary: true do |ansible_config|
    ansible_config.vm.provider "virtualbox" do |vb|
        vb.memory = "2048"
        vb.cpus = 1
        vb.name = "ansibleTempBug"
    end

    ansible_config.vm.box = "bento/ubuntu-16.04"
    ansible_config.vm.host_name = 'ansibleTempBug'
    ansible_config.vm.network "private_network", ip: "192.168.50.9"
    ansible_config.vm.synced_folder "ansible", "/srv/ansible"
    ansible_config.vm.provision :shell, path: "bootstrap.sh"
  end
    
  config.vm.define :node do |node_config|
    node_config.vm.provider "virtualbox" do |vb|
        vb.memory = "2048"
        vb.cpus = 1
        vb.name = "node"
    end

    node_config.vm.box = "marcinbojko/w10-1709en"
    node_config.vm.hostname = "node"
    node_config.vm.network "private_network", ip: "192.168.50.11"
    node_config.vm.provision "shell", path: "ConfigureRemotingForAnsible.ps1", privileged: true
    node_config.vm.network :forwarded_port, guest: 3389, host: 3389, disabled: true
  end
end
