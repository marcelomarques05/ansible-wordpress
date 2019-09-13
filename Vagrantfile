Vagrant.configure("2") do |config|
 
  config.vbguest.auto_update = false
  
  config.vm.define"apache" do |apache|
    apache.vm.box = "centos/7"
    apache.vm.network "private_network", ip: "10.0.11.11"
    apache.vm.network "forwarded_port", guest: 80, host: 8082
    apache.vm.hostname = "apache"
    apache.vm.provider :virtualbox do |vb|
      vb.name = "apache"
      vb.customize ["modifyvm", :id, "--memory", "512"]
      vb.customize ["modifyvm", :id, "--cpus", "2"]
    apache.vm.provision :shell, inline: "yum update -y"
    apache.vm.provision :shell, inline: "setenforce 0", run: "always"
    apache.vm.provision "file", source: "ansible/files/hosts_file", destination: "~/"
    apache.vm.provision "file", source: "ansible/files/sshd_config", destination: "~/"
    apache.vm.provision :shell, inline: "sudo cp /home/vagrant/hosts_file /etc/hosts"
    apache.vm.provision :shell, inline: "sudo cp /home/vagrant/sshd_config /etc/ssh/sshd_config"
    apache.vm.provision :shell, inline: "systemctl restart sshd.service"
      end
  end

  config.vm.define"mysql" do |mysql|
    mysql.vm.box = "centos/7"
    mysql.vm.network "private_network", ip: "10.0.11.12"
    mysql.vm.hostname = "mysql"
    mysql.vm.provider :virtualbox do |vb|
      vb.name = "mysql"
      vb.customize ["modifyvm", :id, "--memory", "512"]
      vb.customize ["modifyvm", :id, "--cpus", "2"]
    mysql.vm.provision :shell, inline: "yum update -y"
    mysql.vm.provision :shell, inline: "setenforce 0", run: "always"
    mysql.vm.provision "file", source: "ansible/files/hosts_file", destination: "~/"
    mysql.vm.provision "file", source: "ansible/files/sshd_config", destination: "~/"
    mysql.vm.provision :shell, inline: "sudo cp /home/vagrant/hosts_file /etc/hosts"
    mysql.vm.provision :shell, inline: "sudo cp /home/vagrant/sshd_config /etc/ssh/sshd_config"
    mysql.vm.provision :shell, inline: "systemctl restart sshd.service"
      end
  end

  config.vm.post_up_message = "Provision finished. :)"
end