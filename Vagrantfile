# -*- mode: ruby -*-
# # vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.ssh.insert_key = false

  if Vagrant.has_plugin?("vagrant-hostmanager")
    config.hostmanager.enabled = true
    config.hostmanager.manage_host = true
    config.hostmanager.ignore_private_ip = false
    config.hostmanager.include_offline = true
  end

  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :machine
  end

  config.vm.define "couchbase" do |vmconfig|
    vmconfig.vm.box = "bento/centos-6.7"
    vmconfig.vm.provider "virtualbox" do |v|
      v.memory = 2048
      v.cpus = 4
    end

    vmconfig.vm.hostname = "couchbase.vagrant"
    vmconfig.vm.network :private_network, ip: "192.168.56.40"

    vmconfig.vm.provision "base", type: "ansible" do |ansible|
      ansible.playbook = "base.yml"
    end

    vmconfig.vm.provision "couchbase", type: "ansible" do |ansible|
      ansible.playbook = "couchbase.yml"
    end
  end

  config.vm.define "nifi" do |vmconfig|
    vmconfig.vm.box = "bento/centos-6.7"
    vmconfig.vm.provider "virtualbox" do |v|
      v.memory = 2048
      v.cpus = 4
    end

    vmconfig.vm.hostname = "nifi.vagrant"
    vmconfig.vm.network :private_network, ip: "192.168.56.20"

    vmconfig.vm.provision "base", type: "ansible" do |ansible|
      ansible.playbook = "base.yml"
    end

    vmconfig.vm.provision "nifi", type: "ansible" do |ansible|
      ansible.playbook = "nifi.yml"
    end
  end
end
