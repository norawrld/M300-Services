# M300-Services
![image](https://github.com/norawrld/M300-Services/assets/87812697/b40aabf0-6ebe-473b-b6d2-c8bd764377f8)

Config File meiner Vagrant VM:

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"

  config.vm.provider "virtualbox" do |vb|
    vb.name = "OracleVM"
    vb.memory = "4096"
    vb.cpus = 2
  end

  # Portweiterleitung für SSH
  config.vm.network "forwarded_port", guest: 22, host: 22, host_ip: "127.0.0.1", auto_correct: true


  # Alle nicht-öffentlichen Ports blockieren
  config.vm.network :forwarded_port, guest: 1, host: 1, protocol: "tcp", auto_correct: true
  config.vm.network :forwarded_port, guest: 1, host: 1, protocol: "udp", auto_correct: true

 
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get -y install apache2
  SHELL
end

![image](https://github.com/norawrld/M300-Services/assets/87812697/5ecda9aa-8b5c-4e1d-9cae-fd5c18e650a1)
