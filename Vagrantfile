BOX_IMAGE = "ubuntu/trusty64"
WEB_COUNT = 2

Vagrant.configure("2") do |config|

  (1..WEB_COUNT).each do |i|

    config.vm.provision :docker
    config.vm.provision :docker_compose

    config.vm.box = BOX_IMAGE

    config.vm.define "svmb#{i}" do |subconfig|
      subconfig.vm.hostname = "svmb#{i}"
      subconfig.vm.network :private_network, ip: "192.168.123.#{i}0"
	    subconfig.vm.synced_folder "config", "/home/vagrant"
      subconfig.vm.provision "shell", inline: <<-SHELL
      mkdir /docker-mail
      cd /docker-mail
      sudo cp /home/vagrant/docker-compose.yml /docker-mail/docker-compose.yml
      sudo echo "DOMAINNAME=tandem#{i}.nitinankeel.ch" > .env
      sudo docker pull tvial/docker-mailserver:latest
      sudo curl -o /docker-mail/setup.sh https://raw.githubusercontent.com/tomav/docker-mailserver/master/setup.sh
      sudo chmod a+x /docker-mail/setup.sh
      sudo echo "/docker-mail/setup.sh email add testuser@tandem#{i}.nitinankeel.ch 1234 \ndocker-compose up -d mail" > startfile.sh
      sudo chmod +x /docker-mail/startfile.sh
      SHELL

      subconfig.vm.provider "virtualbox" do |v|
        v.name = "svmb#{i}"
        v.memory = 512
      end

    end

  end

end