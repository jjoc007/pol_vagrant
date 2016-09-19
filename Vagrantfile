# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/trusty64"
  config.vm.hostname = "ambiente-pol"

  ssh_public_key = File.read(File.join(Dir.home, ".ssh", "id_rsa.pub"))
 
  #Fix SSH forwarded port
  config.vm.network "forwarded_port", guest: 22, host:32222, id: "ssh", auto_correct: true
 
  #Use Apache
  config.vm.network "forwarded_port", guest: 80, host:38080, id: "apache", auto_correct: true
 
  #Use Admin 
  config.vm.network "forwarded_port", guest: 9443, host:29443
 
  #Use Admin debug
  config.vm.network "forwarded_port", guest: 8893, host:28893
 
  #Use Apostgres
  config.vm.network "forwarded_port", guest: 5432, host:35432
 


  config.vm.define "continuous_integration" do |continuous_integration|
   
   config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    echo "#{ssh_public_key}" >> /home/vagrant/.ssh/authorized_keys
    echo "POL_ITERACIONES=671775" >> /etc/environment
    echo "POL_KEY='GuEDXkTZ.6!@u.v2mq3'" >> /etc/environment
    echo "POL_SAL='-8c=GfMBX8U!!VkuX'" >> /etc/environment
    echo "SKIP_LIQUIBASE=true" >> /etc/environment
    echo "M2_HOME=/home/dev/tools/maven3" >> /etc/environment
    echo "M2_REPO=$M2_HOME/repository" >> /etc/environment
    echo "PATH=$PATH:$JAVA_HOME/bin:$M2_HOME/bin" >> /etc/environment
    echo "GS_HOME=/home/dev/servers/gigaspaces-xap-10.0.1" >> /etc/environment
    echo "JSHOMEDIR=/home/dev/servers/gigaspaces-xap-10.0.1" >> /etc/environment
    echo "GS_HOME=/home/dev/servers/gigaspaces-xap-premium-10.0.1-ga" >> /etc/environment
    echo "JSHOMEDIR=/home/dev/servers/gigaspaces-xap-premium-10.0.1-ga" >> /etc/environment
    echo "POLV3_HOME=/home/dev/pol" >> /etc/environment
    echo "MAVEN_HOME=$POLV3_HOME/maven-1.0.2" >> /etc/environment
    echo "JPDA_ADDRESS=8099" >> /etc/environment
    echo "JPDA_TRANSPORT=dt_socket" >> /etc/environment
    echo "PATH=$PATH:$MAVEN_HOME/bin" >> /etc/environment
    echo "JSHOMEDIRV3=$POLV3_HOME/gigaspaces-xap-premium-9.6.2-ga" >> /etc/environment
    echo "MAVEN_HOME_LOCAL=/home/dev/tools/maven1" >> /etc/environment
    echo "JAVA_HOME=/usr/lib/jvm/java-7-oracle" >> /etc/environment

   SHELL

  
    continuous_integration.vm.provision "ansible" do |ansible|
      ansible.inventory_path = "ansible/pol/inventory"
      ansible.verbose = 'vvv'
      ansible.playbook = "ansible/pol.yml"
    end
 
    config.vm.provider "virtualbox" do |v|
      v.memory = 2048
    end
  end

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

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"
  config.vm.synced_folder "/home/dev/tools/maven1", "/home/dev/tools/maven1"
  config.vm.synced_folder "/home/dev/pol", "/home/dev/pol"
  config.vm.synced_folder "/home/dev/payu", "/home/dev/payu"
  config.vm.synced_folder "/home/dev/git/pagosonline", "/home/dev/git/pagosonline"
  config.vm.synced_folder "/home/dev/db_pol", "/home/dev/db_pol"
  config.vm.synced_folder "/home/dev/git/ts_utils", "/home/dev/git/ts_utils"
  config.vm.synced_folder "/home/dev/git/pagosonlinepps", "/home/dev/git/pagosonlinepps"
  

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   sudo apt-get update
  #   sudo apt-get install -y apache2
  # SHELL
end
