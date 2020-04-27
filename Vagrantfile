$install_ANSIBLE = <<-SCRIPT
    sudo apt-add-repository -y ppa:ansible/ansible-2.7
    sudo apt update
    sudo apt-get install ansible -y
    sudo apt install python-minimal -y
SCRIPT

$install_FREE5G = <<-SCRIPT
    sudo apt update
    sudo apt install build-essential -y
    sudo apt-get install manpages-dev
    sudo apt-get install gcc

    curl -O https://dl.google.com/go/go1.11.4.linux-amd64.tar.gz
    sha256sum go1.11.4.linux-amd64.tar.gz
    tar xvf go1.11.4.linux-amd64.tar.gz
    sudo chown -R root:root ./go
    sudo mv go /usr/local
    echo 'export GOPATH=$HOME/work' >> .profile
    echo 'export PATH=$PATH:/usr/local/go/bin:$GOPATH/bin' >> .profile

    sudo apt install qemu-system-x86 -y

    sudo apt-get -y install mongodb wget git
    sudo systemctl start mongodb
    sudo sh -c "cat << EOF > /etc/systemd/network/99-free5gc.netdev
    [NetDev]
    Name=uptun
    Kind=tun
    EOF"

    sudo systemctl enable systemd-networkd
    sudo systemctl restart systemd-networkd
    sudo sh -c "echo 'net.ipv6.conf.uptun.disable_ipv6=0' > /etc/sysctl.d/30-free5gc.conf"
    sudo sysctl -p /etc/sysctl.d/30-free5gc.conf

    sudo sh -c "cat << EOF > /etc/systemd/network/99-free5gc.network
    [Match]
    Name=uptun
    [Network]
    Address=45.45.0.1/16
    Address=cafe::1/64
    EOF"

    sudo systemctl enable systemd-networkd
    sudo systemctl restart systemd-networkd

    sudo apt-get -y install net-tools

    sudo apt-get -y install autoconf libtool gcc pkg-config git flex bison libsctp-dev libgnutls28-dev libgcrypt-dev libssl-dev libidn11-dev libmongoc-dev libbson-dev libyaml-dev

    git clone https://github.com/baleeiro17/free5gcore-configurations.git

    cd free5gmano
    autoreconf -iv
    ./configure --prefix=`pwd`/install
    make -j `nproc`
    make install

SCRIPT


Vagrant.configure("2") do |vm_conf|
    #macedo
    vm_conf.vm.define "macedo" do |config|
        config.vm.provider "virtualbox"
        config.vm.box = "ubuntu/xenial64"
        config.vm.network "private_network", ip:  "192.168.50.11"
        config.vm.provision "shell", inline: $install_ANSIBLE
    end

   #free5g
   vm_conf.vm.define "free5g" do |config|
        config.vm.provider "virtualbox"
        config.vm.box = "ubuntu/bionic64"
        config.vm.network "public_network", ip:  "192.168.50.12"
        #config.vm.provision "shell", inline: $install_FREE5G
    end
end
