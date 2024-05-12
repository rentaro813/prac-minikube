# coding: utf-8
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  # Minikube仮想マシンの起動
  # このディレクトリに予めshareディレクトリを作っておく
  config.vm.define 'minikube' do |machine|
    machine.vm.box = "bento/ubuntu-20.04"
    machine.vm.hostname = 'minikube-makedesmodk8s'
    machine.vm.network :private_network,ip: "172.16.10.11"
    config.vm.network "forwarded_port", guest: 30929, host: 30929
    config.vm.network "forwarded_port", guest: 8880, host: 8880 #http
    config.vm.synced_folder "./share", "/vagrant_data"
    machine.vm.provider "virtualbox" do |vbox|
      vbox.gui = false        
      vbox.cpus = 2
      vbox.memory = 2048
    end

    ## Ansible
    #
    machine.vm.provision "ansible_local" do |ansible|
      ansible.playbook       = "minikube.yml"
      ansible.version        = "latest"      
      ansible.verbose        = false
      ansible.install        = true
      ansible.limit          = "minikube"      
      ansible.inventory_path = "hosts"
    end
  end
end
