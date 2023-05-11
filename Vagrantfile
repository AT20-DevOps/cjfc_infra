$script = <<-SCRIPT
echo "I like Vagrant"
echo "I love Linux"
touch file3
SCRIPT

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
  config.vm.provision :shell, path: "bootstrap.sh"
  config.vm.provision :file, source: "newFile", destination: "newfile"
  config.vm.provision :file, source: "html", destination: "HTMLDIR"
  
  config.vm.define "server-1" do |dockerserver|
    dockerserver.vm.network "private_network", ip: '192.168.56.60'
    dockerserver.vm.hostname = "dockerserver"
    dockerserver.vm.provision :shell, inline: "echo Hi Class from Shell inline"
    dockerserver.vm.provision :shell, inline: $script
    dockerserver.vm.provision "shell" do |s|
      s.inline = "echo $1"
      s.args = ["AT", "Class!"]
    end
    dockerserver.vm.provision "docker" do |d|
      d.run "hello-world"
    end
  end
end
