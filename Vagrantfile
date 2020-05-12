# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  # Configure network
  config.vm.network "private_network", ip: "192.168.33.10"
  # Config root access via private key
  config.vm.provision "shell", inline: <<-SHELL
    sudo mkdir -p /root/.ssh
    sudo cp /vagrant/key.pub /root/.ssh/authorized_keys
    sudo sed -i 's/#PermitRootLogin yes/PermitRootLogin yes/' /etc/ssh/sshd_config
    sudo sed -i 's/#PubkeyAuthentication yes/PubkeyAuthentication yes/' /etc/ssh/sshd_config
    sudo systemctl restart sshd
    sudo yum install -y https://centos7.iuscommunity.org/ius-release.rpm 
    sudo yum install -y python36u python36u-pip python36u-devel
    sudo yum -y groupinstall "GNOME Desktop" "Graphical Administration Tools"
    sudo ln -sf /lib/systemd/system/runlevel5.target /etc/systemd/system/default.target
  SHELL
  config.vm.provider "virtualbox" do |v|
    v.gui = true
  end
end
