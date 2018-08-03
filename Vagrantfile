# -*- mode: ruby -*-
# vi: set ft=ruby :

$KUBE1_IP = "172.16.137.2"
$KUBE2_IP = "172.16.137.3"
$KUBE3_IP = "172.16.137.4"

ANSIBLE_RAW_SSH_ARGS = []

ANSIBLE_RAW_SSH_ARGS << " -o IdentityFile=./.vagrant/machines/kube1/virtualbox/private_key "
ANSIBLE_RAW_SSH_ARGS << " -o IdentityFile=./.vagrant/machines/kube2/virtualbox/private_key "
ANSIBLE_RAW_SSH_ARGS << " -o IdentityFile=./.vagrant/machines/kube3/virtualbox/private_key "

Vagrant.configure("2") do |config|
  config.vm.define "kube1" do |kube1|
    kube1.vm.box = "ubuntu/xenial64"
    kube1.vm.hostname = "kube1"
    kube1.vm.network "private_network", ip: $KUBE1_IP

    kube1.vm.provider :virtualbox do |v, override|
      v.gui = false
      v.customize ["modifyvm", :id, "--cpus", 2]
      v.customize ["modifyvm", :id, "--memory", 2048]
      v.customize ["modifyvm", :id, "--cableconnected1", "on"]
      v.customize ["modifyvm", :id, "--cableconnected2", "on"]
    end

    kube1.vm.provision "shell", inline: "apt-get install -y python"
  end

  config.vm.define "kube2" do |kube2|
    kube2.vm.box = "ubuntu/xenial64"
    kube2.vm.hostname = "kube2"
    kube2.vm.network "private_network", ip: $KUBE2_IP

    kube2.vm.provider :virtualbox do |v, override|
      v.gui = false
      v.customize ["modifyvm", :id, "--cpus", 2]
      v.customize ["modifyvm", :id, "--memory", 2048]
      v.customize ["modifyvm", :id, "--cableconnected1", "on"]
      v.customize ["modifyvm", :id, "--cableconnected2", "on"]
    end

    kube2.vm.provision "shell", inline: "apt-get install -y python"
  end

  config.vm.define "kube3" do |kube3|
    kube3.vm.box = "ubuntu/xenial64"
    kube3.vm.hostname = "kube3"
    kube3.vm.network "private_network", ip: $KUBE3_IP

    kube3.vm.provider :virtualbox do |v, override|
      v.gui = false
      v.customize ["modifyvm", :id, "--cpus", 2]
      v.customize ["modifyvm", :id, "--memory", 2048]
      v.customize ["modifyvm", :id, "--cableconnected1", "on"]
      v.customize ["modifyvm", :id, "--cableconnected2", "on"]
    end

    kube3.vm.provision "shell", inline: "apt-get install -y python"
    kube3.vm.provision "ansible" do |ansible|
      ansible.playbook = "ansible/site.yml"
      ansible.inventory_path = "ansible/inventory"
      ansible.become = true
      ansible.limit = "all"
      ansible.raw_ssh_args = ANSIBLE_RAW_SSH_ARGS
    end
  end
end
