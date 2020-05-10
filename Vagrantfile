# -*- mode: ruby -*-
# vi: set ft=ruby :
VAGRANT_API_VERSION = "2"

instance_IP     = "192.168.35.60"
host_name       = "jenkins"
box             = "ubuntu/bionic64"

Vagrant.configure(VAGRANT_API_VERSION) do |config|

  config.vm.define host_name do |instance|
    instance.vm.box = box
    instance.vm.hostname = host_name
    instance.vm.network :private_network, ip: instance_IP

    instance.vm.synced_folder ".", "/home/vagrant/src", :mount_options => ["dmode=755,fmode=755"]

    # instance.vm.synced_folder './keys', "/home/vagrant/keys", :mount_options => ["fmode=400"]
    instance.vm.network "forwarded_port",id: "jenkins", guest: 8081, host: 8081

    instance.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 1024]
    end

    instance.vm.provision "shell", inline: <<-SCRIPT
      apt-get update -y
      apt-get install docker docker.io docker-compose -y

      usermod -aG docker vagrant
      systemctl start docker
      
      # Run docker compose 
      #su vagrant
      #cd /vagrant
      #docker-compose up -d
    SCRIPT
  end

end
