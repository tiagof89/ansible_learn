# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

servers=[
  {
    :hostname => "ansiblehost1",
    #:ip => "192.168.100.10",
    :box => "ubuntu/xenial64",
    :ram => 1024,
    :cpu => 2
  },
  {
    :hostname => "ansiblehost2",
    #:ip => "192.168.100.11",
    :box => "ubuntu/xenial64",
    :ram => 2048,
    :cpu => 4
  }
]

Vagrant.configure(2) do |config|
    servers.each do |machine|
        config.vm.define machine[:hostname] do |node|
            node.vm.box = machine[:box]
            node.vm.hostname = machine[:hostname]
            #node.vm.network "private_network", ip: machine[:ip]
            node.vm.network :public_network, bridge: "wlp4s0"#, :use_dhcp_assigned_default_route => true
            node.vm.provider "virtualbox" do |vb|
                vb.customize ["modifyvm", :id, "--memory", machine[:ram]]
            end
            config.ssh.forward_agent = true
            config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"
        end
    end
end