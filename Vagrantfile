# -*- mode: ruby -*-
# vi: set ft=ruby :

default_network_interface = `ip route | awk '/^default/ {printf "%s", $5; exit 0}'`

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/bionic64"
  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    # vb.customize [ "modifyvm", :id, "--uartmode1", "disconnected" ]
  end

  config.vm.synced_folder ".", "/vagrant", disabled: true
 
  config.vm.define "lb" do |lb|
  	lb.vm.hostname = "loadbalancer"
 	lb.vm.network "public_network", ip: "192.168.2.120", bridge: default_network_interface
        lb.vm.provider "virtualbox" do |vb|
		vb.name = "k8s-loadbalancer"
		vb.customize ["modifyvm", :id, "--memory", "256"]
	end
  end
 
  config.vm.define "master1" do |master1|
  	master1.vm.hostname = "k8s-master-1"
  	master1.vm.network "public_network", ip: "192.168.2.121", bridge: default_network_interface
        master1.vm.provider "virtualbox" do |vb|
		vb.name = "k8s-master-1"
	end
  end

  config.vm.define "master2" do |master2|
  	master2.vm.hostname = "k8s-master-2"
  	master2.vm.network "public_network", ip: "192.168.2.122", bridge: default_network_interface
        master2.vm.provider "virtualbox" do |vb|
		vb.name = "k8s-master-2"
	end
  end

  config.vm.define "master3" do |master3|
  	master3.vm.hostname = "k8s-master-3"
  	master3.vm.network "public_network", ip: "192.168.2.123", bridge: default_network_interface
        master3.vm.provider "virtualbox" do |vb|
		vb.name = "k8s-master-3"
	end
  end

  config.vm.define "node1" do |node1|
        node1.vm.hostname = "k8s-node-1"
        node1.vm.network "public_network", ip: "192.168.2.110", bridge: default_network_interface
        node1.vm.provider "virtualbox" do |vb|
                vb.name = "k8s-node-1"
        end
  end

  config.vm.define "node2" do |node2|
        node2.vm.hostname = "k8s-node-2"
        node2.vm.network "public_network", ip: "192.168.2.111", bridge: default_network_interface
        node2.vm.provider "virtualbox" do |vb|
                vb.name = "k8s-node-2"
        end
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ssh.yaml"
  end

end
