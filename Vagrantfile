# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vbguest.iso_path = "/Applications/VirtualBox.app/Contents/MacOS/VBoxGuestAdditions.iso"
    config.vbguest.no_remote = true
    
    if Vagrant.has_plugin?("vagrant-cachier")
        config.cache.scope = :box
        config.cache.auto_detect = true
    end
    
    servers = [
        {
            :hostname => "debian1",
            :box => "debian/stretch64",
            :ram => 1024,
            :cpu => 2,
        },
        {
            :hostname => "debian2",
            :box => "debian/stretch64",
            :ram => 1024,
            :cpu => 2,
        },
        {
            :hostname => "debian3",
            :box => "debian/stretch64",
            :ram => 1024,
            :cpu => 2,
        }
    ].each do |machine|
        config.vm.define machine[:hostname] do |node|
            node.vm.box = machine[:box]
            node.vm.hostname = machine[:hostname]
            node.vm.network "private_network", type: "dhcp"

            node.vm.provider :virtualbox do |vb|
                vb.customize ["modifyvm", :id, "--memory", machine[:ram]]
                vb.customize ["modifyvm", :id, "--cpus", machine[:cpu]]
                vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
                vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
            end
        end
    end
end
