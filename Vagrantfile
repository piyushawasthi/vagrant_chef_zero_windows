# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "mwrock/Windows2016"
  config.vm.guest = :windows
  config.vm.communicator = "winrm"
  
  config.vm.boot_timeout = 3600


  # Admin user name and password
  config.winrm.username = 'vagrant'
  config.winrm.password = 'vagrant'

  config.windows.halt_timeout = 15

  # Configure open ports
  config.vm.network :forwarded_port,
                    guest: 3389,
                    host: 3389,
                    id: 'rdp',
                    auto_correct: true

  config.vm.network :forwarded_port,
                    guest: 22,
                    host: 2222,
                    id: 'ssh',
                    auto_correct: true

  config.ssh.private_key_path = "~/.vagrant.d/insecure_private_key"
  # config.vm.provider :virtualbox do |vb|
  #   vb.name = vm_hostname
  # end
  config.ssh.forward_agent = true

  config.vm.provision "chef_zero" do |chef|
    chef.cookbooks_path = "cookbooks"
    chef.nodes_path = "nodes"
    
    chef.add_recipe "apache"
    chef.add_recipe "php-windows"

    chef.add_role "web"
  end
end
