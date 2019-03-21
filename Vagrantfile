Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/bionic64"
    config.vm.define "docker-server"
    config.vm.box_check_update = true

    config.vm.network "public_network", ip: "192.168.1.1"
    config.vm.network "private_network", ip: "10.10.10.10"

    config.vm.synced_folder "./", "/home/vagrant/docker/"

    config.vm.provider "virtualbox" do |vb|
        vb.name = "docker-virtual-machine"
        vb.memory = "1024"
    end

    config.vm.provision "shell", inline: <<-SHELL
        sudo apt-get update && sudo apt-get -y upgrade
        sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
        curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
        sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable" -y
        sudo apt-get update
        sudo apt-get install docker-ce -y
        sudo curl -L https://github.com/docker/compose/releases/download/1.23.0-rc1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
        sudo chmod +x /usr/local/bin/docker-compose
        sudo usermod -aG docker vagrant
    SHELL
end
