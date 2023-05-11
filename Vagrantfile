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
  config.vm.provision :shell, path: "bootstrap.sh"
  config.vm.provision :file, source: "newFile", destination: "newfile"
  config.vm.provision :file, source: "html", destination: "HTMLDIR"
  
  config.vm.define "server-1" do |dockerserver1|
    dockerserver1.vm.network "private_network", ip: '192.168.56.60'
    dockerserver1.vm.hostname = "ci-server"
  end

  config.vm.define "server-2" do |dockerserver2|
    dockerserver2.vm.network "private_network", ip: '192.168.56.60'
    dockerserver2.vm.hostname = "server-2"
    dockerserver2.vm.provision :shell, inline: "echo Hi Class from Shell inline"
    dockerserver2.vm.provision "docker" do |d|
      d.build_dir = "./AT20_COMPILER_SERVICE"
    end
  end
end
