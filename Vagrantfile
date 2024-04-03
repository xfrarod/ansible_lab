# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.provision "shell", run: "always", inline: <<-SHELL
    sudo yum install python3 -y
    sudo yum install net-tools -y
  SHELL

  # config.vm.network "public_network", 
  #   use_dhcp_assigned_default_route: true

  config.vm.define "host1" do |host1|
    host1.vm.box = "centos/7"
    host1.vm.hostname = "host1"
    host1.vm.network "public_network", type: "dhcp", bridge: "en1: Wi-Fi"
  end

  config.vm.define "host2" do |host2|
    host2.vm.box = "centos/7"
    host2.vm.hostname = "host2"
    host2.vm.network "public_network", type: "dhcp", bridge: "en1: Wi-Fi"
  end

end
