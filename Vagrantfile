Vagrant.configure("2") do |config|
  # Load Balancer
  config.vm.define "lb" do |lb|
    lb.vm.box = "ubuntu/bionic64"
    lb.vm.network "private_network", ip: "192.168.56.10" # REPLACE IP ADDRESS

    lb.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y nginx
    SHELL

    lb.vm.provision "file", source: "nginx.conf", destination: "/tmp/nginx.conf"

    lb.vm.provision "file", source: "nginx-default.conf", destination: "/tmp/nginx-default.conf"

    lb.vm.provision "shell", inline: <<-SHELL
      sudo mv /tmp/nginx.conf /etc/nginx/nginx.conf
      sudo mv /tmp/nginx-default.conf /etc/nginx/sites-available/default
      systemctl restart nginx
    SHELL
  end

  # Web Server 1
  config.vm.define "web1" do |web1|
    web1.vm.box = "ubuntu/bionic64"
    web1.vm.network "private_network", ip: "192.168.56.11" # REPLACE IP ADDRESS
    web1.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y apache2
      echo "<h1>Web Server 1</h1>" > /var/www/html/index.html
      systemctl restart apache2
    SHELL
  end

  # Web Server 2
  config.vm.define "web2" do |web2|
    web2.vm.box = "ubuntu/bionic64"
    web2.vm.network "private_network", ip: "192.168.56.12" # REPLACE IP ADDRESS
    web2.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y apache2
      echo "<h1>Web Server 2</h1>" > /var/www/html/index.html
      systemctl restart apache2
    SHELL
  end 

end
