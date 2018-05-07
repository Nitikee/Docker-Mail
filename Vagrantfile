BOX_IMAGE = "ubuntu/trusty64"
WEB_COUNT = 2
Vagrant.configure("2") do |config|
  (1..WEB_COUNT).each do |i|
    config.vm.provision :docker
    config.vm.provision :docker_compose
    config.vm.box = BOX_IMAGE
    config.vm.define "svmb#{i}" do |subconfig|
      subconfig.vm.hostname = "svmb#{i}"
      subconfig.vm.network :private_network, ip: "192.168.1.#{i}0"
	  subconfig.vm.synced_folder "tandem#{i}", "/home/vagrant"
      subconfig.vm.provision "shell", inline: <<-SHELL
      mkdir /docker-mail
      cd /docker-mail
      cp /home/vagrant/docker-compose.yml /docker-mail/docker-compose.yml
      docker pull tvial/docker-mailserver:latest
      sudo curl -o setup.sh https://raw.githubusercontent.com/tomav/docker-mailserver/master/setup.sh
      sudo chmod a+x /docker-mail/setup.sh
      sudo /docker-mail/setup.sh email add "test@tandem1.nitinankeel.ch" 1234 && docker-compose up -d
      SHELL
      subconfig.vm.provider "virtualbox" do |v|
        v.name = "svmb#{i}"
        v.memory = 512
      end
    end
  end
end