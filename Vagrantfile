# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

require 'yaml'
servers = YAML.load_file('servers.yml')

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.synced_folder ".", "/home/vagrant/sync", disabled: true

  servers.each do |servers|
    config.vm.define servers["name"] do |srv|
      srv.vm.box = servers["box"]
      srv.vm.hostname = servers["name"]
      srv.vm.network "private_network", ip: servers["ip"]
      if servers["name"] == "lb"
        srv.vm.network :forwarded_port, guest: 80, host: 8037
      end
      srv.vm.provider :virtualbox do |vb|
        vb.name = servers["name"]
        vb.memory = servers["ram"]
      end
      srv.vm.synced_folder "./ansible", "/home/vagrant/ansible", type: "rsync"
      # Run Ansible from the Vagrant VM
      srv.vm.provision "ansible_local" do |ansible|
        ansible.provisioning_path = "/home/vagrant/ansible"
        ansible.playbook = servers["ansible"]+".yml"
      end
    end
  end
end
