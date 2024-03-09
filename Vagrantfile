# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'yaml'

current_dir = File.dirname(File.expand_path(__FILE__))
configs = YAML.load_file("#{current_dir}/config.yml")
vagrant_config = configs['configs']

Vagrant.configure("2") do |config|

  config.vm.provider "virtualbox" do |v|
    v.memory = vagrant_config['memory']
    v.cpus = vagrant_config['cpus']
  end

  base_ip = vagrant_config['base_ip'].split('.')[0..-2].join('.')
  last_octet = vagrant_config['base_ip'].split('.').last.to_i

  vagrant_config['nodes'].each_with_index do |node_config, index|
    config.vm.define node_config['name'] do |node|
      config.vm.boot_timeout = 600
      node.vm.hostname = node_config['name']
      node.vm.network "public_network", ip: "#{base_ip}.#{last_octet + index}"
      node.vm.box = vagrant_config['box']

      node.vm.provision "ansible" do |ansible|
        ansible.playbook = node_config['playbook']
        if node_config['name'] == 'ntp-client'
          ansible.host_vars = {
            node_config['name'] => {
              "ntp_server_ip" => vagrant_config['base_ip']
            }
          }
        end
      end
    end
  end
end