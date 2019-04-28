Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.define "collector" do |collector|
    collector.vm.network :private_network, ip: "192.168.70.10"
      collector.vm.provider "virtualbox" do |vb|
        vb.gui = false
        vb.name = "collector"
        vb.memory = "1024"
      end
    config.vm.provision "shell", inline: <<-SHELL
      hostnamectl set-hostname collector
      yum -y install wget net-tools
      cd /etc/yum.repos.d
      wget https://raw.githubusercontent.com/theo-bot/Labsession/master/infludata.repo
    SHELL
  end
end
