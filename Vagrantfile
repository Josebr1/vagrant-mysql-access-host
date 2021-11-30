$script_mysql_install = <<-SCRIPT
  apt-get update && \
  apt-get install mysql-server-5.7 && \
  mysql < /Vagrant/mysql/script/user.sql && \
  mysql < /Vagrant/mysql/script/schema.sql && \
  mysql < /Vagrant/mysql/script/data.sql && \
  cat /Vagrant/mysql/mysqld.cnf > /etc/mysql/mysql.conf.d/mysqld.cnf && \
  service mysql restart
SCRIPT

Vagrant.configure("2") do |config|
  
  config.vm.box = "ubuntu/bionic64"

  config.vm.define "mysqlserver" do |mysqlserver|
    mysqlserver.vm.network "private_network", ip: "10.10.0.15"
    mysqlserver.vm.network "forwarded_port", guest: 3306, host: 3306

    mysqlserver.vm.provider "virtualbox" do |vb|
      vb.name = "mysqlserver"
    end

    mysqlserver.vm.provision "shell", inline: $script_mysql_install
  end
  
end
