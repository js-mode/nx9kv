BOX = "nxosv-9.2.3.box"

Vagrant.configure("2") do |config|

    # Deploy 3 Nodes

    config.vm.define "n9k1" do |node|

        node.vm.box = BOX
        # When booting a n9000v box from scratch this actually works!
        node.vm.base_mac = "0800276CEEAA"

        # node.vm.network "public_network", auto_config: false
        # node.vm.provision "shell", run: "always", inline: "ip address 10.10.0.199/24"
        # node.vm.network "public_network", bridge: "en0: Ethernet"
        # port forward for ssh and nxapi https calls
        node.vm.network "forwarded_port", guest: 22, host: 2221, auto_correct: true, id: "ssh"
        node.vm.network "forwarded_port", guest: 443, host: 4431, auto_correct: true

        # eth1/1 connected to nxeth121, auto-config not supported.
        node.vm.network :private_network, virtualbox__intnet: "nxeth121", auto_config: false

        # eth1/2 connected to nxeth122, auto-config not supported.
        node.vm.network :private_network, virtualbox__intnet: "nxeth122", auto_config: false

        # eth1/3 connected to nxeth131, auto-config not supported.
        node.vm.network :private_network, virtualbox__intnet: "nxeth131", auto_config: false

        node.vm.provider "virtualbox" do |v|
            # v.customize ["modifyvm", :id, "--memory", "4096"]
            v.customize ["modifyvm", :id, "--name", "n9k1"]
            v.customize ["modifyvm", :id, "--vram", "24"]
            v.customize ["modifyvm", :id, "--cpus", "1"]
            v.customize ["modifyvm", :id, "--uartmode1", "server", '/tmp/n9k1']
            # v.customize ["modifyvm", :id, "--nic1", "bridged"]
            v.customize ["modifyvm", :id, "--nicpromisc2", "allow-all"]
            v.customize ["modifyvm", :id, "--nicpromisc3", "allow-all"]
            v.customize ["modifyvm", :id, "--nicpromisc4", "allow-all"]
        end
    end

    config.vm.define "n9k2" do |node|
        node.vm.box = BOX
        # When booting a n9000v box from scratch this actually works!
        node.vm.base_mac = "0800276DEEAA"

        # port forward for ssh and nxapi https calls
        node.vm.network "forwarded_port", guest: 22, host: 2222, auto_correct: true, id: "ssh"
        node.vm.network "forwarded_port", guest: 443, host: 4432, auto_correct: true

        # eth1/1 connected to nxeth121, auto-config not supported.
        node.vm.network :private_network, virtualbox__intnet: "nxeth121", auto_config: false

        # eth1/2 connected to nxeth122, auto-config not supported.
        node.vm.network :private_network, virtualbox__intnet: "nxeth122", auto_config: false

        # eth1/3 connected to nxeth231, auto-config not supported.
        node.vm.network :private_network, virtualbox__intnet: "nxeth231", auto_config: false

        node.vm.provider "virtualbox" do |v|
            v.customize ["modifyvm", :id, "--name", "n9k2"]
            v.customize ["modifyvm", :id, "--vram", "24"]
            v.customize ["modifyvm", :id, "--cpus", "1"]
            v.customize ["modifyvm", :id, "--uartmode1", "server", '/tmp/n9k2']
            v.customize ["modifyvm", :id, "--nicpromisc2", "allow-all"]
            v.customize ["modifyvm", :id, "--nicpromisc3", "allow-all"]
            v.customize ["modifyvm", :id, "--nicpromisc4", "allow-all"]
        end
    end

    config.vm.define "n9k3" do |node|
        node.vm.box = BOX
        # When booting a n9000v box from scratch this actually works!
        node.vm.base_mac = "0800276EEEAA"

        # port forward for ssh and nxapi https calls
        node.vm.network "forwarded_port", guest: 22, host: 2223, auto_correct: true, id: "ssh"
        node.vm.network "forwarded_port", guest: 443, host: 4433, auto_correct: true

        # eth1/1 connected to nxeth131, auto-config not supported.
        node.vm.network :private_network, virtualbox__intnet: "nxeth131", auto_config: false

        # eth1/2 connected to nxeth231, auto-config not supported.
        node.vm.network :private_network, virtualbox__intnet: "nxeth231", auto_config: false

        node.vm.provider "virtualbox" do |v|
            v.customize ["modifyvm", :id, "--name", "n9k3"]
            v.customize ["modifyvm", :id, "--vram", "24"]
            v.customize ["modifyvm", :id, "--cpus", "1"]
            v.customize ["modifyvm", :id, "--uartmode1", "server", '/tmp/n9k3']
                        v.customize ["modifyvm", :id, "--nicpromisc2", "allow-all"]
            v.customize ["modifyvm", :id, "--nicpromisc3", "allow-all"]
        end
    end

end