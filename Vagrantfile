Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.provision :docker
  config.vm.provision :docker_compose
  config.vm.network "public_network", ip: "10.71.10.30"
  config.vm.synced_folder "home", "/home/vagrant"
  config.vm.provision "shell", inline: <<-SHELL
  sudo cp /home/vagrant/hosts /etc/hosts
SHELL
end