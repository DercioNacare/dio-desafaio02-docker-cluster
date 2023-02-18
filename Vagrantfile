machines = {
  "master" => {"memory" => "1024", "cpu" => "1", "ip" => "192.168.56.50", "image" => "bento/ubuntu-22.04"},
  "node01" => {"memory" => "1024", "cpu" => "1", "ip" => "192.168.56.51", "image" => "bento/ubuntu-22.04"},
}

Vagrant.configure("2") do |config|

  machines.each do |name, conf|
    config.vm.define "#{name}" do |machine|
      machine.vm.box = "#{conf["image"]}"
      machine.vm.hostname = "#{name}"
      machine.vm.network "private_network", ip: "#{conf["ip"]}"
      machine.vm.provider "virtualbox" do |vb|
        vb.name = "#{name}"
        vb.memory = conf["memory"]
        vb.cpus = conf["cpu"]
        
      end
      machine.vm.provision "shell", path: "instalar-docker.sh"
      
      if "#{name}" == "master"
        machine.vm.provision "shell", path: "config-master.sh"
      else
        machine.vm.provision "shell", path: "config-works.sh"
      end
    end
  end
end