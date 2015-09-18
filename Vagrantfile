# -*- mode: ruby -*-
# vi: set ft=ruby :

# you're doing.
Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty32"
  config.vm.network "forwarded_port", guest: 80, host: 80
  config.vm.network "private_network", ip: "10.10.10.11"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "512"
  end
  config.vm.provision "file", source: "nginx.config", destination: "nginx.config"
  config.vm.provision "shell", inline: <<-SHELL
    curl -sL https://deb.nodesource.com/setup | sudo bash -
    sudo apt-get upgrade -y
    sudo apt-get install -y zip nginx
    curl -L https://ghost.org/zip/ghost-latest.zip -o ghost.zip
    sudo mkdir /var/www
    sudo mkdir /var/www/ghost
    sudo chown vagrant:vagrant /var/www/ghost
    sudo unzip -uo ghost.zip -d /var/www/ghost
    cd /var/www/ghost
    sudo apt-get install -y nodejs
    sudo npm install --production
    CC=gcc-4.9 CXX=g++-4.9 npm install sqlite3
    sudo npm install -g forever
    sudo cat /vagrant/nginx.config | sudo tee /etc/nginx/sites-available/default
    sudo service nginx restart
    sudo cat /vagrant/ghost.config | sudo tee /var/www/ghost/config.js
    NODE_ENV=production sudo forever start index.js
    echo DONE.
    echo Acess Ghost at http://10.10.10.11 and http://10.10.10.11/ghost
  SHELL
end
