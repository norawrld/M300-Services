Vagrant

![image](https://github.com/norawrld/M300-Services/assets/87812697/93e2733c-9ab4-4929-b6fd-5fee52643aa1)

Installation Apache Webserver automatisiert:

# Install Apache web server
    sudo apt-get -y install apache2

# Enable necessary Apache modules
    sudo a2enmod proxy
    sudo a2enmod proxy_http

Apache Webserver Status:

sudo systemctl status apache2
![image](https://github.com/norawrld/M300-Services/assets/87812697/19d7990d-a642-4dfa-8eed-7282450ac9be)

![image](https://github.com/norawrld/M300-Services/assets/87812697/9d521910-bdf4-4144-a931-00d8f58bf545)

Installation MySQL automatisiert:

sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password password mypassword'
sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password mypassword'
sudo apt-get -y install php libapache2-mod-php php-curl php-cli php-mysql php-gd mysql-client mysql-server
    
MySQL Status:

sudo service mysql status
![image](https://github.com/norawrld/M300-Services/assets/87812697/2ede414d-3897-4338-92de-8aafb4f1a2cc)


![image](https://github.com/norawrld/M300-Services/assets/87812697/501c7300-75f0-440c-91c7-e68c6810bea3)

![image](https://github.com/norawrld/M300-Services/assets/87812697/809e4b62-6c70-4204-a311-53a045de3b59)

Netzwerkplan

![image](https://github.com/norawrld/M300-Services/assets/87812697/0f826a03-0c79-4102-a448-c75a5daf78ba)

