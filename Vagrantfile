# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "opscode-centos-6.5"

  # The url from where the 'config.vm.box' box will be fetched if it
  # doesn't already exist on the user's system.
  config.vm.box_url = "http://opscode-vm-bento.s3.amazonaws.com/vagrant/virtualbox/opscode_centos-6.5_chef-provisionerless.box"

  # Override settings for specific providers
  config.vm.provider :virtualbox do |vb, override|
    vb.name = "civicrm"
    vb.customize ["modifyvm", :id, "--memory", "1024"]
  end

  config.vm.hostname = "civicrm"

  config.vm.provider :aws do |aws, override|
    aws.access_key_id = "EXAMPLE"
    aws.secret_access_key = "EXAMPLE"
    aws.keypair_name = "default"
    aws.security_groups = ["default"]
    aws.instance_type = 'm1.small'
    aws.ami = "ami-e7582d8e"
    aws.tags = { Name: 'Vagrant civicrm' }

    override.ssh.username = "ubuntu"
    override.ssh.private_key_path = "EXAMPLE_PATH"
  end

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  config.vm.network :forwarded_port, guest: 80, host: 9020

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network :private_network, ip: "33.33.33.111"

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "provisioning/site.yml"
    ansible.inventory_path = "provisioning/hosts"
    #ansible.verbose = "vv"
  end
end