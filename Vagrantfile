# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box_url = "https://vagrantcloud.com/ubuntu/xenial64"
  config.vm.box = "ubuntu/xenial64"

  config.vm.hostname = "vagrant-security"
  config.vm.network :private_network, type: "dhcp"

  config.vm.provision "shell", inline: "sudo apt-get -y update && sudo apt-get install -y laptop-detect && sudo apt-get -y install python"

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.tags = "security"
  end

  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :machine
  end

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  end
end
