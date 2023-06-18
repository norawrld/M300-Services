Config meiner Vagrant Datei:


Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"

  config.vm.provider "virtualbox" do |vb|
    vb.name = "ContainerModul300"
    vb.memory = "4096"
    vb.cpus = 2
  end

  # Port forwarding for SSH
  config.vm.network "forwarded_port", guest: 22, host: 22, host_ip: "127.0.0.1", auto_correct: true

  # Port forwarding for HTTP
  config.vm.network "forwarded_port", guest: 80, host: 8080

  # Provisioning shell script
  config.vm.provision "shell", inline: <<-SHELL
    # Update the system
    sudo apt-get update

    # Install Apache web server
    sudo apt-get -y install apache2

    # Enable necessary Apache modules
    sudo a2enmod proxy
    sudo a2enmod proxy_http

    # Configure Apache reverse proxy
    sudo sh -c 'echo "ProxyPass \"/app1/\" \"http://backend1:8080/\"" >> /etc/apache2/sites-available/000-default.conf'
    sudo sh -c 'echo "ProxyPassReverse \"/app1/\" \"http://backend1:8080/\"" >> /etc/apache2/sites-available/000-default.conf'
    sudo sh -c 'echo "ProxyPass \"/app2/\" \"http://backend2:8080/\"" >> /etc/apache2/sites-available/000-default.conf'
    sudo sh -c 'echo "ProxyPassReverse \"/app2/\" \"http://backend2:8080/\"" >> /etc/apache2/sites-available/000-default.conf'

    # Install MySQL
    set -o xtrace
    sudo apt-get update
    sudo apt-get -y install debconf-utils 
    sudo apt-get -y install apache2 
    sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password password admin'
    sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password admin'
    sudo apt-get -y install php libapache2-mod-php php-curl php-cli php-mysql php-gd mysql-client mysql-server
    

    # Allow remote access to MySQL (optional, comment out if not needed)
    sudo sed -i "s/bind-address.*/bind-address = 0.0.0.0/" /etc/mysql/mysql.conf.d/mysqld.cnf
    sudo service mysql restart
    
    # Add a new user
    sudo useradd -m -s /bin/bash -G sudo newuser

    # Add a new group
    sudo groupadd newgroup

    # Assign the new user to the new group
    sudo usermod -aG newgroup newuser
    
    # Copy custom index.html file
    sudo cp /vagrant/index.html /var/www/html/

    # Firewall rules
    sudo iptables -F
    sudo iptables -P INPUT DROP
    sudo iptables -P FORWARD DROP
    sudo iptables -P OUTPUT ACCEPT
    sudo iptables -A INPUT -i lo -j ACCEPT
    sudo iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
    sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
    sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
    sudo iptables -A INPUT -p tcp --dport 3306 -j ACCEPT

    # Save firewall rules
    sudo iptables-save | sudo tee /etc/iptables/rules.v4

    # Restart Apache
    sudo systemctl restart apache2
  SHELL
end
