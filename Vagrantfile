# -*- mode: ruby -*-
# vi: set ft=ruby :
$hostsfile_update = <<-'SCRIPT'
echo -e '192.168.58.2 k8s-master-01.example.com k8s-master-01\n192.168.58.3 k8s-master-02.example.com master-02\n192.168.58.11 k8s-worker-01.example.com k8s-worker-01' >> /etc/hosts
SCRIPT

IMAGE_NAME = "bento/ubuntu-20.04"
M = 2
W = 1

Vagrant.configure("2") do |config|
    config.ssh.insert_key = true
    config.vm.provider "virtualbox" do |vm|
        vm.customize ["modifyvm", :id, "--audio", "none"]
        vm.customize ["modifyvm", :id, "--vram", "64"]
        vm.customize ["modifyvm", :id, "--graphicscontroller", "vmsvga"]
        vm.customize ["modifyvm", :id, "--accelerate3d", "on"]
        vm.memory = 2048
        vm.cpus = 2
    end

    (1..M).each do |i|
        config.vm.define "k8s-master-0#{i}" do |worker|
            worker.vm.box = IMAGE_NAME
            worker.vm.network "private_network", ip: "192.168.58.#{i + 1}"
            worker.vm.hostname = "k8s-master-0#{i}"
            worker.vm.provision "shell", inline: $hostsfile_update
            # worker.vm.provision "ansible" do |ansible|
            #     ansible.playbook = "provisioning/k8s-master.yml"
            # end
        end
    end


    (1..W).each do |i|
        config.vm.define "k8s-worker-0#{i}" do |master|
            master.vm.box = IMAGE_NAME
            master.vm.network "private_network", ip: "192.168.58.#{i + 10}"
            master.vm.hostname = "k8s-worker-0#{i}"
            master.vm.provision "shell", inline: $hostsfile_update
            # master.vm.provision "ansible" do |ansible|
            #     ansible.playbook = "provisioning/k8s-worker.yml"
            # end
        end
    end

end
