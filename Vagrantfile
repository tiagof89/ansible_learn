# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.define "assuratest" do |machine|

    # Prevent synchronization of /tmp strangely tried when provisioning centos/7 box
    config.vm.synced_folder '/tmp/', '/vagrant', disabled: true

    # All Vagrant configuration is done here. The most common configuration options are documented and commented below.
    # For a complete reference, please see the online documentation at vagrantup.com.

    machine.vm.box = "ubuntu/xenial64"
    
    # Create a private network, which allows host-only access to the machine using a specific IP.
    machine.vm.network :private_network, ip: "192.168.56.17"

    # Create a public network, which generally matched to bridged network.
    # Bridged networks make the machine appear as another physical device on your network.
    # machine.vm.network :public_network

    # If true, then any SSH connections made will enable agent forwarding. Default value: false
    # machine.ssh.forward_agent = true

    # Share an additional folder to the guest VM. The first argument is the path on the host to the actual folder.
    # The second argument is the path on the guest to mount the folder. And the optional third argument is a set of
    # non-required options.
    # machine.vm.synced_folder "../data", "/vagrant_data"

    # Provider-specific configuration so you can fine-tune various backing providers for Vagrant. These expose provider-
    # specific options. View the documentation for the provider you're using for more information on available options.
    machine.vm.provider :virtualbox do |v|
      v.name = "assura-test"
      v.gui = false  # Headless mode
      v.cpus = 2
      v.memory = 2048
            v.customize [
        "modifyvm", :id,
        "--cpus", "2",
        "--memory", "2048",
        "--hwvirtex", "on",
        "--ioapic", "on"
      ]
    end

    config.ssh.forward_agent = true
    config.vm.provision "file", source: "repo_key", destination: "/home/ubuntu/.ssh/repo_key"

    config.vm.provision "shell", path: "script.sh" 

  end
  end
