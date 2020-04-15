$install_5GCORE = <<-SCRIPT
    sudo apt-add-repository -y ppa:ansible/ansible-2.7
    sudo apt update
    sudo apt-get install ansible -y
    sudo apt install python-minimal -y
SCRIPT

Vagrant.configure("2") do |config_5gcore|
   #core5G
   config_5gcore.vm.define "core5G" do |config|
      config.vm.provider "virtualbox"
      config.vm.box = "ubuntu/xenial64"
      config.vm.network "public_network", ip:  "192.168.50.11"
      config.vm.provision "shell", inline: $install_5GCORE
  end
end
