Vagrant.configure("2") do |config|
    config.vm.provision "shell", inline: <<-SHELL
        apt-get update -y
        echo "10.0.0.10  master-node" >> /etc/hosts
        echo "10.0.0.11  worker-node01" >> /etc/hosts
    SHELL
    
    config.vm.define "master" do |master|
      master.vm.box = "bento/ubuntu-18.04"
      master.vm.hostname = "master-node"
      master.vm.network "private_network", ip: "10.0.0.10"
      master.vm.provider "virtualbox" do |vb|
          vb.memory = 4048
          vb.cpus = 2
      end
      master.vm.provision "shell", path: "scripts/common.sh"
      master.vm.provision "shell", path: "scripts/master.sh"
    end

  
    config.vm.define "node0" do |node|
      node.vm.box = "bento/ubuntu-18.04"
      node.vm.hostname = "worker-node-0"
      node.vm.network "private_network", ip: "10.0.0.11"
      node.vm.provider "virtualbox" do |vb|
          vb.memory = 2048
          vb.cpus = 1
      end
      node.vm.provision "shell", path: "scripts/common.sh"
      node.vm.provision "shell", path: "scripts/node.sh"
    end
    
  end
