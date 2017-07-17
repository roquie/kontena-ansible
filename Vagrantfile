# -*- mode: ruby -*-
# vi: set ft=ruby :

# ======================================
#
# USE ONLY FOR DEVELOPMENT
#
# ======================================

# @link: http://docs.ansible.com/ansible/guide_vagrant.html

boxes = [
  {
    :name => "ubuntu16",
    :box  => "ubuntu/xenial64",
    :ip   => "10.110.0.10",
    :cpu  => 66,
    :ram  => 512,
    :p80_host => 7100,
    :p443_host => 7101
  },
  {
    :name => "ubuntu14",
    :box  => "ubuntu/trusty64",
    :ip   => "10.110.0.11",
    :cpu  => 66,
    :ram  => 512,
    :p80_host => 7100,
    :p443_host => 7101
  }
]

Vagrant.configure("2") do |config|
  boxes.each do |box|
    config.vm.define box[:name] do |vms|
      vms.vm.host_name = box[:name]
      vms.vm.box = box[:box]
      vms.vm.box_url = box[:url]

      vms.vm.provider "virtualbox" do |v|
        v.customize ["modifyvm", :id, "--cpuexecutioncap", box[:cpu]]
        v.customize ["modifyvm", :id, "--memory", box[:ram]]
      end

      vms.vm.provision "shell" do |s|
        ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
        s.inline = <<-SHELL
          sudo mkdir -p /root/.ssh/ && sudo touch /root/.ssh/authorized_keys
          echo #{ssh_pub_key} >> /root/.ssh/authorized_keys
          sudo sed -i -E 's/PermitRootLogin(.*)/PermitRootLogin yes/g' /etc/ssh/sshd_config
          sudo service sshd restart
        SHELL
      end

      vms.vm.network :forwarded_port, guest: 80, host: box[:p80_host]
      vms.vm.network :forwarded_port, guest: 443, host: box[:p443_host]
      vms.vm.network :private_network, ip: box[:ip]
    end
  end
end
