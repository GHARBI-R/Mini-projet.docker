# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.vm.define "master" do |master|
      master.vm.box = "geerlingguy/centos7"
      master.vm.network "public_network", type: "static", ip: "192.168.43.20"
      master.vm.hostname = "master"
      master.vm.provider "virtualbox" do |v|
        v.name = "master"
        v.memory = 4096
        v.cpus = 2
      end
      master.vm.provision :shell do |shell|
        shell.path = "install_swarm.sh"
        shell.args = ["master", "192.168.43.20"]
      end
    end
    workers=1
    ram_worker=2048
    cpu_worker=2
    (1..workers).each do |i|
      config.vm.define "worker#{i}" do |worker|
        worker.vm.box = "geerlingguy/centos7"
        worker.vm.network "public_network", type: "static", ip: "192.168.43.2#{i}"
        worker.vm.hostname = "worker#{i}"
        worker.vm.provider "virtualbox" do |v|
          v.name = "worker#{i}"
          v.memory = ram_worker
          v.cpus = cpu_worker
        end
        worker.vm.provision :shell do |shell|
          shell.path = "install_swarm.sh"
          shell.args = ["node", "192.168.43.20"]
        end
      end
    end
  end