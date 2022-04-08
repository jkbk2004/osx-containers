Vagrant.configure("2") do |config|
    config.vm.box = "generic/ubuntu1810"

    config.vm.define 'ubuntu'

    # Prevent SharedFoldersEnableSymlinksCreate errors
    config.vm.synced_folder ".", "/vagrant", disabled: true
    # Enable X-Forwarding
    config.ssh.forward_agent = true
    config.ssh.forward_x11 = true
end
