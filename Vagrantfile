# -*- mode: ruby -*-
# vi: set ft=ruby :
machines = {
  "master" => {"memory" => 512, "cpu" => "1", "ip" => "10" ,"image" => "ubuntu/lunar64"},
  "node"   => {"memory" => 512, "cpu" => "1", "ip" => "11" ,"image" => "ubuntu/lunar64"},
  "node2"  => {"memory" => 512, "cpu" => "1", "ip" => "12" ,"image" => "ubuntu/lunar64"}
}

Vagrant.configure("2") do |config|
  machines.each do |name, conf|
    config.vm.define "#{name}" do |machine|
      machine.vm.box = "#{conf["image"]}"
      machine.vm.hostname = "#{name}"
      machine.vm.network "private_network", ip: "192.168.56.#{conf["ip"]}"
      machine.vm.provider "virtualbox" do |vb|
        vb.name = "#{name}"
        vb.memory = conf["memory"]
        vb.cpus = conf["cpu"]
      end
      machine.vm.provision "shell", path: "/home/rodrigo/Documentos/lab-desafio/instalar-docker.sh"
      
      if("#{name}" == "master")
        machine.vm.provision "shell", path: "/home/rodrigo/Documentos/lab-desafio/master.sh"
      else
        machine.vm.provision "shell", path: "/home/rodrigo/Documentos/lab-desafio/worker.sh"
      end
      
    end
  end
end

