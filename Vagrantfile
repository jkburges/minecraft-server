# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.omnibus.chef_version = :latest
  config.vm.box = "hashicorp/precise64"

  config.vm.provision "chef_solo" do |chef|
    chef.add_recipe "minecraft"
  end

end
