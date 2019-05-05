Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.define "db1" do |db1|
    db1.vm.network :private_network, ip: "192.168.70.10"
      db1.vm.provider "virtualbox" do |vb|
        vb.gui = false
        vb.name = "db1"
        vb.memory = "1024"
      end
    config.vm.provision "shell", inline: <<-SHELL
      hostnamectl set-hostname db1
      yum -y install wget net-tools 
      cd /etc/yum.repos.d
      wget https://raw.githubusercontent.com/theo-bot/Labsession/master/infludata.repo
      echo '+@users:ALL' >> /etc/security/access.conf
      cp /etc/ssh/sshd_config /etc/ssh/sshd_config.orig
      sed 's/PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config.orig > /etc/ssh/sshd_config
      useradd proxy -g users -G wheel
      echo "secret" | passwd --stdin proxy
      systemctl restart sshd
      wget https://raw.githubusercontent.com/theo-bot/Labsession/master/hosts -O /etc/hosts 
    SHELL
  end
  config.vm.define "db2" do |db2|
    db2.vm.network :private_network, ip: "192.168.70.20"
    config.vm.provision "shell", inline: <<-SHELL
      hostnamectl set-hostname db2
      yum -y install wget net-tools 
      cd /etc/yum.repos.d
      wget https://raw.githubusercontent.com/theo-bot/Labsession/master/infludata.repo
      echo '+@users:ALL' >> /etc/security/access.conf
      cp /etc/ssh/sshd_config /etc/ssh/sshd_config.orig
      sed 's/PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config.orig > /etc/ssh/sshd_config
      useradd proxy -g users -G wheel
      echo "secret" | passwd --stdin proxy
      systemctl restart sshd
      wget https://raw.githubusercontent.com/theo-bot/Labsession/master/hosts -O /etc/hosts
    SHELL
  end
  config.vm.define "gui" do |gui|
    gui.vm.network :private_network, ip: "192.168.70.30"
    config.vm.provision "shell", inline: <<-SHELL
      hostnamectl set-hostname gui
      yum -y install wget net-tools 
      cd /etc/yum.repos.d
      wget https://raw.githubusercontent.com/theo-bot/Labsession/master/grafana.repo
      echo '+@users:ALL' >> /etc/security/access.conf
      cp /etc/ssh/sshd_config /etc/ssh/sshd_config.orig
      sed 's/PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config.orig > /etc/ssh/sshd_config
      useradd proxy -g users -G wheel
      echo "secret" | passwd --stdin proxy
      systemctl restart sshd
      wget https://raw.githubusercontent.com/theo-bot/Labsession/master/hosts -O /etc/hosts
    SHELL
  end
  config.vm.define "relay" do |relay|
    relay.vm.network :private_network, ip: "192.168.70.40"
    config.vm.provision "shell", inline: <<-SHELL
      hostnamectl set-hostname relay
      yum -y install wget net-tools 
      echo '+@users:ALL' >> /etc/security/access.conf
      cp /etc/ssh/sshd_config /etc/ssh/sshd_config.orig
      sed 's/PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config.orig > /etc/ssh/sshd_config
      useradd proxy -g users -G wheel
      echo "secret" | passwd --stdin proxy
      systemctl restart sshd
      wget https://raw.githubusercontent.com/theo-bot/Labsession/master/hosts -O /etc/hosts
    SHELL
  end
end
