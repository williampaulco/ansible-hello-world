# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  $script = <<~'SCRIPT'
    echo "These are my \"quotes\"! I am provisioning my guest."
    date > /etc/vagrant_provisioned_at
  SCRIPT

  config.vm.define 'controller' do |node|
    node.vm.box = 'ubuntu/focal64'
    node.vm.hostname = 'controller'
    node.vm.network 'private_network', ip: '192.168.33.20'
    node.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt install software-properties-common
      apt-add-repository --yes --update ppa:ansible/ansible
      apt install ansible -y
    SHELL
  end

  config.vm.define 'winhost' do |node|
    node.vm.box = 'mwrock/Windows2016'
    node.vm.hostname = 'winhost'
    node.vm.network 'private_network', ip: '192.168.33.10'
    node.vm.provision "shell", inline: <<-SHELL
      Set-Item -Path WSMan:\\localhost\\Service\\AllowUnencrypted -Value $true
      Set-Item -Path WSMan:\\localhost\\Service\\Auth\\Basic -Value $true
      Set-Item -Path WSMan:\\localhost\\Client\\AllowUnencrypted -Value $true
      Set-Item -Path WSMan:\\localhost\\Client\\Auth\\Basic -Value $true
    SHELL
  end

end
