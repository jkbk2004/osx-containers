Vagrant.configure("2") do |config|
    config.vm.box = "generic/ubuntu1804"
    
    # Vagrant uses vagrant user by default. Docker uses root. Use root, it is
    # a development environment anyway.
    config.ssh.username = "root"

    config.vm.provider "docker" do |docker|
      # The name of the image to use
      docker.image = "nineseconds/docker-vagrant"

      # vagrant docker images have SSH so why not to use it
      docker.has_ssh = true

      # Yes, containers are long running.
      docker.remains_running = true
    end
        
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
