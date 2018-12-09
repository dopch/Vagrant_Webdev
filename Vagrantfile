# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.hostname = "Nginx-1"
  config.vm.define "Nginx-1"
  #config.vm.provision "shell", path: "provision.sh"
  config.vm.provision "shell", inline: <<-SHELL
                      sudo yum update -y
                      sudo yum install epel-release -y
                      sudo yum install nginx -y
                      sudo systemctl enable nginx
                      sudo systemctl start nginx
                      SHELL
  config.vm.provision "shell", run: "always", inline: <<-SHELL
                      sudo setenforce 0
                      SHELL
  config.vm.network "forwarded_port", guest: 80, host: 8080, id: "nginx"
  config.vm.synced_folder "./webdev/", "/usr/share/nginx/",
                          owner: "vagrant",
                          group: "nginx" 
end
