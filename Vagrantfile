#Setting BOX_IMAGE for all VMs"
BOX_IMAGE = "ubuntu/trusty64"

#Setting numbers of webserver to be created
WEB_COUNT = 2

#Vagrant configurations
Vagrant.configure("2") do |config|
  
  #Configurations for the PFSense
  config.vm.define "pfsense" do |subconfig|
    #Get the Box-Image
    subconfig.vm.box = "49thsd/pfsense2.3.4-amd64"
    #Configure name for VM in vagrant --> Not Virtualbox VM name!
    subconfig.vm.hostname = "pfsense"

    #Creating VM Net "LAN" with the netaddress "192.168.1.0/24"
    #If you don't name this network, virtualbox will create a Hostonly adapter --> VM's cant communicate with each other (We dont wan't this)
    subconfig.vm.network :private_network, ip: "192.168.1.1",
    virtualbox__intnet: "LAN1"
	subconfig.vm.network :private_network, ip: "192.168.2.1",
    virtualbox__intnet: "LAN2"
    
    #These are the settings for your virtualbox
    #Configure the virtualbox with VM Name und amount of memmory
    subconfig.vm.provider "virtualbox" do |v|
        v.name = "pfsense"
        v.memory = 1024
      end
  end # End of "pfsense" configuration
=begin
  #Starting configuration for webserver
  #Loop foreach webserver you defined
  (1..WEB_COUNT).each do |i|
    
    #Creating 'i' amount of webserver with the bellow configurations
    config.vm.define "web#{i}" do |subconfig|
      
      #Box-Image
      subconfig.vm.box = BOX_IMAGE

      #Hostname of vagrant vm
      #{i} is a integer -> eg. web1 or web2
      subconfig.vm.hostname = "web#{i}"

      #create Network and asssing IPs
      #{i + 9} --> eg. "i" is equal 1; add 9
      subconfig.vm.network :private_network, ip: "192.168.200.#{i + 9}",
      
      #The name of the network needs to be the same.
      virtualbox__intnet: "LAN"
      
      #Synced foler web1 and web2
      subconfig.vm.synced_folder "web#{i}", "/home/vagrant"

      #Copy the index.html file too the www/html folder from nginx
      #I couldn't make the synced folder in the www/html file because nginx will complain at the installation
      subconfig.vm.provision "shell", inline: <<-SHELL
      cp /home/vagrant/index.html /usr/share/nginx/html/
      SHELL

      #Virtualbox settings
      subconfig.vm.provider "virtualbox" do |v|
        v.name = "web#{i}"
        v.memory = 512
      end
    end
  end #End of Webserver configurations

  #Settings for all machines
  #Install updates
  #Add UFW Rule 80
  #Enable UFW
  #Install NGINX
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo ufw allow 80
    sudo ufw allow 22
    sudo ufw -f enable
    sudo apt-get -y install nginx
  SHELL
=end
end













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
