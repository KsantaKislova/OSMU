Vagrant.configure("2") do |config|

  servers=[
      {
          :hostname => "kislova-ubuntu-1",
          :box => "ubuntu/trusty64",
          :ip => "172.16.1.50",
          :ssh_port => "2200"
      },
      {
          :hostname => "kislova-ubuntu-2",
          :box => "ubuntu/trusty64",
          :ip => "172.16.1.51",
          :ssh_port => "2201"
      }
  ]

  servers.each do |machine|
      config.vm.define machine[:hostname] do |node|
          node.vm.box = machine[:box]
          node.vm.hostname = machine[:hostname]
          node.vm.network :private_network, ip: machine[:ip]
          node.vm.network "forwarded_port", guest: 22, host: machine[:ssh_port], id: "ssh"
          node.vm.synced_folder "C:/Users/asus/Documents/UNIVERSITY/Lab2", "/var/www"
          node.vm.provision "file", source: "./module2.txt", destination: "/var/www/module2.txt"
          node.vm.provision "shell",
          inline: "
          sudo apt-get update && upgrade
          sudo apt-get install git
          git init .
          git remote add -f origin https://github.com/KsantaKislova/OSMU
          git checkout module2
          cat module2.txt
          ping 172.16.1.1
          ping 172.16.1.2
          ",
          privileged: "false"
          node.vm.provider :virtualbox do |vb|
              vb.customize ["modifyvm", :id, "--memory", 1024]
              vb.customize ["modifyvm", :id, "--cpus", 2]
          end
      end
   end
end
