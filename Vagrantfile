# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"


### shell provisioning script ### =========================
$script_node1 = <<SCRIPT
echo node1

sed -i -e '/HOSTNAME/d' /etc/sysconfig/network
echo 'HOSTNAME=node1.dev' >> /etc/sysconfig/network
hostname -f node1.dev

echo "I am node1 server provisining ..."
date > /root/vagrant_provisioned_at

mkdir -p /var/www/test/node01.dev/public_html
chown -R vagrant: /var/www/test/node01.dev/public_html

yum -y install yum-fastestmirror

yum -y install httpd

touch /etc/httpd/conf.d/00_vhost.conf
echo "NameVirtualHost *:80" >> /etc/httpd/conf.d/00_vhost.conf
touch /etc/httpd/conf.d/vhost-node1.dev.conf
echo "<VirtualHost *:80>" >> /etc/httpd/conf.d/vhost-node1.dev.conf
echo "  DocumentRoot /var/www/test/node01.dev/public_html" >> /etc/httpd/conf.d/vhost-node1.dev.conf
echo "</VirtualHost>" >> /etc/httpd/conf.d/vhost-node1.dev.conf

sed -i.bak 's/enabled=0/enabled=1/' /etc/yum.repos.d/epel-testing.repo

yum -y install php \
epel-release \
vim-enhanced \
php-cli \
php-common \
php-devel \
php-gd \
php-intl \
php-mbstring \
php-pdo \
php-pear.noarch \
php-xml \
php-mcrypt
cp -avf /etc/php.ini /etc/php.ini-ORIG
echo "date.timezone = Asia/Tokyo" >> /etc/php.ini
echo "<?php" > /var/www/test/node01.dev/public_html/index.php
echo "  echo \"this is node1.dev host\n\";" >> /var/www/test/node01.dev/public_html/index.php
echo "  phpinfo();" >> /var/www/test/node01.dev/public_html/index.php

chkconfig httpd on
service httpd start

service httpd reload

SCRIPT
### ### =================================


Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  ## config.vm.box = "puphpet/centos65-x64"
  ## config.vm.box_url = "http://conoha.macpoi.me/demo/demo01-vagrant-512mb/centos65-x86_64-20140116.box"
  #
  config.vm.box = "gtb-centos65-x64"
  ## config.vm.box = "puphpet/centos65-x64"
  ## config.vm.box_url = "https://conoha.macpoi.me/demo02/gtb-centos65-x64.box"
  config.vm.box_url = "http://conoha.macpoi.me:10080/demo02/gtb-centos65-x64.box"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # If true, then any SSH connections made will enable agent forwarding.
  # Default value: false
  # config.ssh.forward_agent = true

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"
  #
  config.vm.synced_folder "./share", "/vagrant_data"
  ## config.vm.synced_folder "./source/node01.dev", "/var/www/test/node01.dev", :create => true, :owner => 'vagrant', :group => 'vagrant', :extra => 'dmode=777,fmode=666'
  config.vm.synced_folder "./source/node01.dev", "/var/www/test/node01.dev", :create => true, :owner => 'vagrant', :group => 'vagrant', :mount_options => ['dmode=777', 'fmode=666']
  ##

  # sudo yum install docker-io

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Don't boot with headless mode
  #   vb.gui = true
  #
  #   # Use VBoxManage to customize the VM. For example to change memory:
  #   vb.customize ["modifyvm", :id, "--memory", "1024"]
  # end
  config.vm.provider "virtualbox" do |vb|
    # Don't boot with headless mode
    ## vb.gui = true
    vb.gui = false
  
    # Use VBoxManage to customize the VM. For example to change memory:
    ## vb.customize ["modifyvm", :id, "--memory", "1024"]
    ## vb.customize ["modifyvm", :id, "--memory", "512"]
  end

  config.vm.define :node1 do |cur_node|
    ## for 64bit vm
    ## cur_node.vm.box = "centos6"
    ## for 32bit vm
    ## cur_node.vm.box = "centos6-i386"
    cur_node.vm.hostname = "node1.dev"
    #
    cur_node.vm.network :forwarded_port, guest: 22, host: 2201, id: "ssh"
    cur_node.vm.network :forwarded_port, guest: 80, host: 8001, id: "http"
    cur_node.vm.network :private_network, ip: "192.168.33.11"

    cur_node.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--memory", "512"]
      vb.name = "node1"
    end

    #cur_node.vm.provision "shell" do |shell|
    #  #shell.inline: "echo node1"
    #  #shell.inline: "sed -i -e '/HOSTNAME/d' /etc/sysconfig/network"
    #  #shell.inline: "echo 'HOSTNAME=node1.dev' >> /etc/sysconfig/network"
    #  #shell.inline: "hostname -f node1.dev"
    #end
    cur_node.vm.provision :shell, :inline => $script_node1
  end

  #config.vm.define :node2 do |cur_node|
  #  ## for 64bit vm
  #  ##cur_node.vm.box = "centos6"
  #  ## for 32bit vm
  #  cur_node.vm.box = "centos6-i386"
  #  cur_node.vm.network :forwarded_port, guest: 22, host: 2202, id: "ssh"
  #  cur_node.vm.network :forwarded_port, guest: 80, host: 8002, id: "http"
  #  cur_node.vm.network :private_network, ip: "192.168.33.12"
  #end
  #
  # View the documentation for the provider you're using for more
  # information on available options.

  ## shell script inline
  ## config.vm.provision :shell, :inline => $script_node1

  # Enable provisioning with CFEngine. CFEngine Community packages are
  # automatically installed. For example, configure the host as a
  # policy server and optionally a policy file to run:
  #
  # config.vm.provision "cfengine" do |cf|
  #   cf.am_policy_hub = true
  #   # cf.run_file = "motd.cf"
  # end
  #
  # You can also configure and bootstrap a client to an existing
  # policy server:
  #
  # config.vm.provision "cfengine" do |cf|
  #   cf.policy_server_address = "10.0.2.15"
  # end

  # Enable provisioning with Puppet stand alone.  Puppet manifests
  # are contained in a directory path relative to this Vagrantfile.
  # You will need to create the manifests directory and a manifest in
  # the file default.pp in the manifests_path directory.
  #
  # config.vm.provision "puppet" do |puppet|
  #   puppet.manifests_path = "manifests"
  #   puppet.manifest_file  = "site.pp"
  # end

  # Enable provisioning with chef solo, specifying a cookbooks path, roles
  # path, and data_bags path (all relative to this Vagrantfile), and adding
  # some recipes and/or roles.
  #
  # config.vm.provision "chef_solo" do |chef|
  #   chef.cookbooks_path = "../my-recipes/cookbooks"
  #   chef.roles_path = "../my-recipes/roles"
  #   chef.data_bags_path = "../my-recipes/data_bags"
  #   chef.add_recipe "mysql"
  #   chef.add_role "web"
  #
  #   # You may also specify custom JSON attributes:
  #   chef.json = { :mysql_password => "foo" }
  # end

  # Enable provisioning with chef server, specifying the chef server URL,
  # and the path to the validation key (relative to this Vagrantfile).
  #
  # The Opscode Platform uses HTTPS. Substitute your organization for
  # ORGNAME in the URL and validation key.
  #
  # If you have your own Chef Server, use the appropriate URL, which may be
  # HTTP instead of HTTPS depending on your configuration. Also change the
  # validation key to validation.pem.
  #
  # config.vm.provision "chef_client" do |chef|
  #   chef.chef_server_url = "https://api.opscode.com/organizations/ORGNAME"
  #   chef.validation_key_path = "ORGNAME-validator.pem"
  # end
  #
  # If you're using the Opscode platform, your validator client is
  # ORGNAME-validator, replacing ORGNAME with your organization name.
  #
  # If you have your own Chef Server, the default validation client name is
  # chef-validator, unless you changed the configuration.
  #
  #   chef.validation_client_name = "ORGNAME-validator"
end
