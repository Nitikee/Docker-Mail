# Docker-Mail

Nitinan Keel </br>
Containerization of application and services </br>
Docker-Mail

## Table of contents
* [Concept]
  * [Requierements]
  * [Networkdiagramm]
  * [IP-Table]
  * [DNS]
* [Installation]
  * [Setup folders and required files]
  * [Vagrantfiles]
* [Testing]
* [Project review]

## Concept

### Requirements:
* [Vagrant](https://www.vagrantup.com/downloads.html)
* [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
* [Git](https://git-scm.com/download/win)
* [Vagrant plugin](https://github.com/leighmcculloch/vagrant-docker-compose)

### Networkdiagramm
```
                                     +------------------------+
                                     | SVMB1                  |
                   SMTP --> 25  +----+ 192.168.1.10/24        |
                   IMAP --> 143 |    | tandem2.nitinankeel.ch |
+----------------+              |    +------------------------+
| Windows Client +--------------+
| 192.168.1.2/24 |              |    +------------------------+
+----------------+              |    | SVMB2                  |
                                +----+ 192.168.1.20/24        |
                                     | tandem1.nitinankeel.ch |
                                     +------------------------+
```
### DNS Records
```
 +-------------------------------------------------------------+
 | DNS Server                                                  |
 | ns1.hostserv.eu                                             |
 |                                                             |
 | A Record                                                    |
 | mail.tandem1.nitinankeel.ch ==> 192.168.1.10/24             |
 | mail.tandem2.nitinankeel.ch ==> 192.168.1.20/24             |
 | tandem1.nitinankeel.ch      ==> 192.168.1.10/24             |
 | tandem2.nitinankeel.ch      ==> 192.168.1.20/24             |
 |                                                             |
 | MX Record                                                   |
 | tandem1.nitinankeel.ch      ==> mail.tandem1.nitinankeel.ch |
 | tandem2.nitinankeel.ch      ==> mail.tandem2.nitinankeel.ch |
 +-------------------------------------------------------------+
```

### Setup folders and required files
```
. 
├── tandem1         
|   ├── docker-compose.yml
│   └── user.sh
├── tandem2
|   ├── docker-compose.yml
│   └── user.sh         
├── LICENSE (GPLv2)
└── Vagrantfile               # Vagrant file
```
### Vagrantfile
```RUBY
# BOX Image is Trusty64
BOX_IMAGE = "ubuntu/trusty64"
# Mail Node Server
WEB_COUNT = 2¨
# Start Vagrant configuration
Vagrant.configure("2") do |config|
# Foreach Mail Server
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
      cat /home/vagrant/test.sh | bash
      docker-compose up -d
      SHELL
      subconfig.vm.provider "virtualbox" do |v|
        v.gui = true
        v.name = "svmb#{i}"
        v.memory = 512
      end
    end
  end
  config.vm.provision "shell", inline: <<-SHELL
  echo "hallo"
  SHELL
end
```
## Testing

## Project review