# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
    config.vm.box = "ubuntu/precise64"
    config.vm.define :site do |config|
        config.vm.provider :virtualbox do |v|
            v.customize [ "modifyvm", :id, "--memory", "2200" ]
        end
        config.vm.host_name = "mail.fritz.box"

        # set lavish permission so that everything is executable
        #

        config.vm.synced_folder "sites", "/var/www/sites",
          # :mount_options => ['dmode=755', 'fmode=644'],
          :create => true,
          :nfs => true

        config.vm.network :private_network, type: 'dhcp'
        config.vm.network "public_network", ip: "192.168.178.54", :bridge => 'en1: WLAN (AirPort)'

        config.vm.provision :shell, :path => "provision.sh"
    end
    # https://github.com/mitchellh/vagrant/issues/1673
    config.ssh.pty = true
end
