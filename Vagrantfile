Vagrant.configure("2") do |config|
  config.vm.box = "brahimhamdi/jenkins-ci"

  config.vm.hostname = "jenkins-ci"
  config.vm.network "forwarded_port", guest: 5000, host: 5000
  config.vm.network "forwarded_port", guest: 30000, host: 30000
  config.vm.network "forwarded_port", guest: 22, host: 2222
  config.vm.network :private_network, ip: "192.168.201.100"

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt install apt-transport-https ca-certificates curl software-properties-common
    sudo systemctl disable systemd-resolved
    sudo rm -rf /etc/run/systemd/resolve/stub-resolv.conf /etc/resolv.conf
    sudo echo "nameserver  8.8.8.8" > /etc/resolv.conf
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
    sudo apt update
    sudo apt install -y docker-ce docker-compose
  SHELL
end
