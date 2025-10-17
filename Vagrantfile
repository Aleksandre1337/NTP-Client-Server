# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'yaml'

current_dir = File.dirname(File.expand_path(__FILE__))
configs = YAML.load_file("#{current_dir}/config.yml")['configs']

Vagrant.configure("2") do |config|
  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.provider "virtualbox" do |v|
    v.memory = configs['memory']
    v.cpus = configs['cpus']
    v.customize ["modifyvm", :id, "--uartmode1", "disconnected"]
  end

  configs['nodes'].each do |node|
    config.vm.define node['name'] do |vm|
      vm.vm.hostname = node['name']
      vm.vm.network "public_network", ip: node['ip']
      vm.vm.box = configs['box']
      vm.vm.boot_timeout = 600

      vm.vm.provision "ansible" do |ansible|
        ansible.playbook = "./playbooks/site.yml"
        ansible.inventory_path = "./inventory/vagrant.ini"
        ansible.limit = node['name']
      end
    end
  end
end
