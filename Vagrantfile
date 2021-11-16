# -*- mode: ruby -*-
# vi: set ft=ruby :
$script = <<-SCRIPT
cp /vagrant/daemon.json /etc/docker/daemon.json
mkdir -p /etc/systemd/system/docker.service.d/
cp /vagrant/docker.conf /etc/systemd/system/docker.service.d/docker.conf
systemctl daemon-reload
systemctl enable docker
systemctl restart docker
SCRIPT


Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-21.04"
  config.vm.network "public_network"
  config.vm.provider "parallels" do |prl|
    prl.name = "docker.local"
    prl.memory = 4096
    prl.cpus = 4
  end
  # make docker volumes work
  config.vm.synced_folder "#{Dir.home}", "#{Dir.home}"
  config.vm.provision :docker
  config.vm.provision "shell", inline: $script
end
