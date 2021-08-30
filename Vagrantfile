# -*- mode: ruby -*-
# vi: set ft=ruby :

$script_name = <<-EOF
 sudo apt update
 sudo apt install -y software-properties-common
 sudo add-apt-repository --yes --update ppa:ansible/ansible
 sudo apt install -y ansible

EOF

$hosts_name = <<-EOF
  sudo echo -e "192.168.0.201   ansible
  192.168.0.202   webserver1
  192.168.0.203   webserver2" > /etc/hosts
EOF

Vagrant.configure("2") do |config|
  config.vm.define "ansible" do |server|
    server.vm.box = "ubuntu/xenial64"
    server.vm.hostname = "ansible"
    server.vm.network "public_network", ip: "192.168.0.201", bridge: "wlp9s0"
    server.vm.provider "virtualbox" do |vb|
      vb.name = "ansible"
      vb.memory = 2048
      vb.cpus = 1
      vb.customize ["modifyvm", :id, "--groups", "/Vagrant/Lab-ansible"]
    end
    server.vm.provision "shell", inline: $hosts_name
    server.vm.provision "shell", inline: $script_name
  end

  config.vm.define "webserver1" do |server|
    server.vm.box = "ubuntu/xenial64"
    server.vm.hostname = "webserver1"
    server.vm.network "public_network", ip: "192.168.0.202", bridge: "wlp9s0"
    server.vm.provider "virtualbox" do |vb|
      vb.name = "webserver1"
      vb.memory = 2048
      vb.cpus = 1
      vb.customize ["modifyvm", :id, "--groups", "/Vagrant/Lab-ansible"]
    end
    server.vm.provision "shell", inline: $hosts_name
    server.vm.provision "shell", inline: $script_name
  end
  config.vm.define "webserver2" do |server|
    server.vm.box = "ubuntu/xenial64"
    server.vm.hostname = "webserver2"
    server.vm.network "public_network", ip: "192.168.0.203", bridge: "wlp9s0"
    server.vm.provider "virtualbox" do |vb|
      vb.name = "webserver2"
      vb.memory = 2048
      vb.cpus = 1
      vb.customize ["modifyvm", :id, "--groups", "/Vagrant/Lab-ansible"]
    end
    server.vm.provision "shell", inline: $hosts_name
    server.vm.provision "shell", inline: $script_name
  end
end