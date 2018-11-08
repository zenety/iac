Vagrant.configure("2") do |config|
  # define provider configuration
  config.vm.provider :libvirt do |v|
    v.memory = 1024
  end
  # define a VM configuration
  config.vm.define "raddit-app" do |app|
    app.vm.box = "generic/ubuntu1604"
    app.vm.hostname = "raddit-app"
    # sync a local folder with application code to the VM folder
    app.vm.synced_folder "raddit-app/", "/srv/raddit-app"
    # use port forwarding make application accessible on localhost
    app.vm.network "forwarded_port", guest: 9292, host: 9292
    # system configuration is done by Ansible
    app.vm.provision "ansible" do |ansible|
      ansible.playbook = "ansible/configuration.yml"
    end
  end
end
