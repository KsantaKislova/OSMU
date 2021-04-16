$script = <<-'SCRIPT'
sudo apt-get update && upgrade
sudo apt-get install git -y
git config --global user.name "KsantaKislova"
git config --global user.email kisel.skywalker99@gmail.com
git clone -b module2 https://github.com/KsantaKislova/OSMU.git
SCRIPT

Vagrant.configure("2") do |config|
        config.vm.define "Ubuntu1" do |conf|
          conf.vm.box = "ubuntu/trusty64"
          conf.vm.hostname = "kislovaUbu1"
          conf.vm.network :private_network, ip: "192.168.11.21"

          conf.vm.provider :virtualbox do |vb|
              vb.customize [
                  "modifyvm", :id,
                  "--memory", "1024",
                  "--cpus", "1"
              ]
          end

          conf.vm.provision "shell", inline: $script
end

        config.vm.define "Ubuntu2" do |conf|
          conf.vm.box = "ubuntu/trusty64"
          conf.vm.hostname = "kislovaUbu2"
          conf.vm.network :private_network, ip: "192.168.11.22"

          conf.vm.provider :virtualbox do |vb|
              vb.customize [
                  "modifyvm", :id,
                  "--memory", "1024",
                  "--cpus", "1"
              ]
          end

          conf.vm.provision "shell", inline: $script
      end
  end
