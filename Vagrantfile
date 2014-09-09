# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.omnibus.chef_version = :latest
  config.vm.box = "hashicorp/precise64"

  config.vm.provision "chef_solo" do |chef|

    chef.json = {
      "minecraft" => {
        "accept_eula" => true,
        "ops" => [ "max_fire_2008" ],
        "url" => "https://s3.amazonaws.com/Minecraft.Download/versions/1.8/minecraft_server.1.8.jar",
        "properties" => {
          "gamemode" => 1
        }
      }
    }

    chef.add_recipe "apt"
    chef.add_recipe "java"
    chef.add_recipe "minecraft"

  end

  config.vm.provider :openstack do |os, override|

    override.vm.box = "dummy"
    override.vm.box_url = "https://github.com/cloudbau/vagrant-openstack-plugin/raw/master/dummy.box"

    override.ssh.username = ENV['VAGRANT_USER'] || "ubuntu"
    override.ssh.private_key_path = ENV['VAGRANT_SSH_KEY'] || '~/.ssh/nectar.pem'

    os.username = ENV['VAGRANT_OPENSTACK_USERNAME']
    os.api_key  = ENV['VAGRANT_OPENSTACK_API_KEY']
    os.flavor   = ENV['VAGRANT_OPENSTACK_FLAVOR'] || /m1.small/
    os.image    = ENV['VAGRANT_OPENSTACK_IMAGE'] || "NeCTAR Ubuntu 12.04.4 (Precise) amd64"
    os.endpoint = "https://keystone.rc.nectar.org.au:5000/v2.0/tokens"
    os.keypair_name = ENV['VAGRANT_OPENSTACK_KEYPAIR_NAME'] || 'nectar'
    os.server_name = 'minecraft'

    # os.address_id = 'noblepark'
    # os.scheduler_hints = {
    #   :cell => 'melbourne-qh2'
    # }
    os.tenant = ENV['VAGRANT_OPENSTACK_TENANT'] || 'pt-1219'
    os.security_groups = ['ssh', 'http', 'nrpe', 'minecraft']

  end
end
