# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "ubuntu/trusty64"

  # Web Port forwarding
  config.vm.network "forwarded_port", guest: 80, host: 8000
  # MySQL Port forwarding
  config.vm.network "forwarded_port", guest: 3306, host: 33060

  # generally we are too lazy to copy from host machine ssh keys to guest
  # so we enable forward agent
  config.ssh.forward_agent = true

  # This has to be private network, because nfs wont work otherway
  config.vm.network :private_network, ip: "10.0.0.111"

  # Vagrant is a hell lot faster through nfs and udp enabled
  config.vm.synced_folder ".", "/vagrant",
    id: "core",
    nfs: true,
    mount_options: ['nolock,vers=3,udp,noatime']

  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--memory", "512"]
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
    ansible.sudo = true
    ansible.raw_ssh_args = ["-o UserKnownHostsFile=/dev/null"]
  end
end
