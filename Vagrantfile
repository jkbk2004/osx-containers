Vagrant.configure("2") do |config|
    config.vm.box = "generic/ubuntu1804"

    config.vm.define 'ubuntu'
    config.vm.provision "shell", inline: "sudo mkdir -p ./app"
    #config.vm.provision "shell", inline: "sudo mkdir -p ./vagrant"
    
    config.vm.provider "docker" do |d|
        d.image = "nginx:latest"
        d.ports = [“8080:80”]
        d.name = “nginx-container”
    end
    
    # Prevent SharedFoldersEnableSymlinksCreate errors
    #config.vm.synced_folder ".", "/vagrant", disabled: true
    
    # Share an additional folder to the guest VM. The first argument is
    # the path on the host to the actual folder. The second argument is
    # the path on the guest to mount the folder. And the optional third
    # argument is a set of non-required options.
    config.vm.synced_folder ".", "/home/vagrant/vagrant_data",
       mount_options: ["dmode=775,fmode=777"]
    
    # provision with a basic user environment
    config.vm.provision "environment", type: "shell", privileged: true,
                         inline: <<-EOF
        set -e
        export DEBIAN_FRONTEND=noninteractive
        apt-get update
        apt-get install -y build-essential python3 gcc curl python3-pip
        apt-get install -y autoconf pkg-config libtool autoconf-archive
        apt-get update
    EOF
    
    # provision the VM with docker
    #config.vm.provision "docker"    
    
    # Enable X-Forwarding
    config.ssh.forward_agent = true
    config.ssh.forward_x11 = true
end
