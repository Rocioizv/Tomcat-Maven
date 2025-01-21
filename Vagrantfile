# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.box = "debian/bullseye64"
  config.vm.define "practica" do |practica|
    practica.vm.hostname = "practica"
    practica.vm.network "forwarded_port", guest: 8080, host: 8080
    practica.vm.network "private_network", ip: "192.168.50.20"
    practica.vm.provision "shell", name: "basic_provision", inline: <<-SHELL
        apt-get update
        sudo apt install -y openjdk-11-jdk
        sudo apt install -y tomcat9
        sudo groupadd tomcat9
        sudo useradd -s /bin/false -g tomcat9 -d /etc/tomcat9 tomcat9
        sudo systemctl start tomcat9

        sudo cp /vagrant/conf-practica/tomcat-users.xml /etc/tomcat9/tomcat-users.xml
        sudo apt install -y tomcat9-admin
        sudo cp /vagrant/conf-practica/context.xml /usr/share/tomcat9-admin/host-manager/META-INF/context.xml
        sudo systemctl restart tomcat9

        sudo apt-get update && sudo apt-get -y install maven
        sudo cp /vagrant/conf-practica/settings.xml /etc/maven/settings.xml
        cd /vagrant/tomcat-war
        mvn tomcat7:deploy
        
      SHELL
  end # práctica

end
