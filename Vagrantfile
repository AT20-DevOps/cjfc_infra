# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end

  config.vm.provision :docker
  config.vm.provision :docker_compose

  config.vm.define "ci-server" do |ciserver|
    ciserver.vm.network "private_network", ip: '192.168.56.60'
    ciserver.vm.hostname = "ci-server"
  end

  config.vm.define "server-3" do |dockerserver2|
    dockerserver2.vm.network "private_network", ip: '192.168.56.62'
    dockerserver2.vm.hostname = "server-3"
    dockerserver2.vm.provision :file, source: "AT20_COMPILER_SERVICES", destination: "AT20_COMPILER_SERVICES"
    dockerserver2.vm.provision :file, source: "docker-compose.yml", destination: "docker-compose.yml"
    dockerserver2.vm.provision :file, source: ".env", destination: ".env"
    dockerserver2.vm.provision "shell", inline: "docker compose up -d"
  end
end
