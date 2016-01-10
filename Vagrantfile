# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.ssh.forward_agent = true
  # config.vm.synced_folder Dir.getwd, "/home/vagrant/roles/ansible-mesos", nfs: true
  config.vm.synced_folder ".", "/vagrant"
  # ubuntu 12.04 that Travis CI is using
  # config.vm.define 'travis', primary: true do |c|
  #   c.vm.network "private_network", ip: "192.168.100.2"
  #   c.vm.box = "precise-server-cloudimg-amd64-vagrant-disk1"
  #   c.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/precise/current/precise-server-cloudimg-amd64-vagrant-disk1.box"
  #   c.vm.provision "shell" do |s|
  #     s.inline = "apt-get update -y; apt-get install python-software-properties; add-apt-repository ppa:rquillo/ansible; apt-get update -y; apt-get install ansible -y"
  #     s.privileged = true
  #   end
  # end

  MESOS_SLAVE_COUNT= ENV['MESOS_SLAVE_COUNT'] || 2

  # ubuntu 14.04
  config.vm.define 'ubuntu', primary: true do |c|
    c.vm.network "private_network", ip: "192.168.100.2"
    c.vm.box = "ubuntu/trusty64"
    c.vm.provision "shell" do |s|
      s.inline = "apt-get update -y; apt-get install -y software-properties-common; apt-add-repository ppa:ansible/ansible; \
      apt-get update -y; apt-get install -y ansible;\
      wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | sudo apt-key add -;\
       sh -c 'echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list';
       apt-get update; apt-get install jenkins -y"
      s.privileged = true
    end
    c.vm.provider "virtualbox" do |vb|
       vb.memory = "4096"
    end
  end

  # config.vm.define 'mesos-master', primary: true do |c|
  #   c.vm.network "private_network", ip: "192.168.100.1"
  #   c.vm.hostname = "mesos-master"
  #   c.vm.box = "ubuntu/trusty64"
  #   c.vm.provision :shell, previlidged: true, inline: "cp /vagrant/hosts /etc/hosts"
  #   c.vm.provision :ansible do |ans|
  #     ans.playbook = "mesos-master.yml"
  #     ans.sudo = true
  #     ans.host_key_checking = false
  #   end
  # end
  #
  # config.vm.define 'jenkins-master', primary: true do |c|
  #   c.vm.network "private_network", ip: "192.168.100.8"
  #   c.vm.hostname = "mesos-master"
  #   c.vm.box = "ubuntu/trusty64"
  #   c.vm.provision "file", source: "./hosts", destination: "/etc/hosts"
  #
  #   c.vm.provision :ansible do |ans|
  #     ans.playbook = "jenkins-master.yml"
  #     ans.sudo = true
  #     ans.host_key_checking = false
  #   end
  # end
  #
  # config.vm.define 'zookeeper', primary: true do |c|
  #   c.vm.network "private_network", ip: "192.168.100.3"
  #   c.vm.hostname = "zookeeper"
  #   c.vm.box = "ubuntu/trusty64"
  #   c.vm.provider "virtualbox" do |vb|
  #      vb.memory = "512"
  #   end
  #   c.vm.provision :shell do |s|
  #     s.inline = "cp /vagrant/hosts /etc/hosts"
  #     s.privileged = true
  #   end
  #   c.vm.provision :ansible do |ans|
  #     ans.playbook = "zookeeper.yml"
  #     ans.sudo = true
  #     ans.host_key_checking = false
  #   end
  # end
  # centos 6:
  #
  # config.vm.define 'centos' do |c|
  #   c.vm.network "private_network", ip: "192.168.100.4"
  #   c.vm.box = "centos65-x86_64-20140116"
  #   c.vm.box_url = "https://github.com/2creatives/vagrant-centos/releases/download/v6.5.3/centos65-x86_64-20140116.box"
  #   c.vm.provision "shell" do |s|
  #     s.inline = "yum update gmp; yum install ansible -y"
  #     s.privileged = true
  #   end
  # end

  # centos 7:
  # config.vm.define 'centos7' do |c|
  #   c.vm.network "private_network", ip: "192.168.100.5"
  #   c.vm.box = "centos/7"
  #   c.vm.provision "shell" do |s|
  #     s.inline = "yum install -y epel-release; yum install -y ansible"
  #     s.privileged = true
  #   end
  # end

end
