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
      wget https://raw.githubusercontent.com/theo-bot/Labsession/master/grafana.repo
      echo '+@users:ALL' >> /etc/security/access.conf
      cp /etc/ssh/sshd_config /etc/ssh/sshd_config.orig
      sed 's/PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config.orig > /etc/ssh/sshd_config
      useradd proxy -g users -G wheel
      echo "secret" | passwd --stdin proxy
      systemctl restart sshd
    SHELL
  end
  config.vm.define "vm1" do |vm1|
    vm1.vm.network :private_network, ip: "192.168.70.20"
    config.vm.provision "shell", inline: <<-SHELL
      hostnamectl set-hostname vm1
      yum -y install wget net-tools 
      cd /etc/yum.repos.d
      wget https://raw.githubusercontent.com/theo-bot/Labsession/master/infludata.repo
      wget https://raw.githubusercontent.com/theo-bot/Labsession/master/grafana.repo
      echo '+@users:ALL' >> /etc/security/access.conf
      cp /etc/ssh/sshd_config /etc/ssh/sshd_config.orig
      sed 's/PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config.orig > /etc/ssh/sshd_config
      useradd proxy -g users -G wheel
      echo "secret" | passwd --stdin proxy
      systemctl restart sshd
    SHELL
  end

end
