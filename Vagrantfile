 Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.hostname = "nexus.cdp"
  config.vm.network :private_network, ip: "192.168.56.100"

  config.ssh.insert_key = false

  config.vm.provider "virtualbox" do |vb|
    # Virtual Machine Name
    vb.name = "nexus-playground"
    # Display the VirtualBox GUI when booting the machine
    vb.gui = false
    # Customize the amount of memory on the VM:
    vb.memory = "512"
  end

  config.vm.provision "shell", inline: <<-SHELL
    yum install -y epel-release yum-utils device-mapper-persistent-data lvm2 
    yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
    yum install -y docker-ce python-pip
    pip install -U pip 
    pip install -U docker-compose
    usermod -aG docker $(whoami)
    systemctl enable docker.service
    systemctl start docker.service
    docker-compose version
  SHELL
end
