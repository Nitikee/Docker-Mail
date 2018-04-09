Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.provision :docker
  config.vm.provision :docker_compose
  config.vm.network "forwarded_port", guest: 25, host:25
  config.vm.network "forwarded_port", guest: 143, host:143
  config.vm.synced_folder "home", "/home/vagrant"
  config.vm.provision "shell", inline: <<-SHELL
  sudo cp /home/vagrant/hosts /etc/hosts
SHELL
end
