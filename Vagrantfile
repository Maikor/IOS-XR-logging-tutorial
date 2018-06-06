# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure(2) do |config|

  config.vm.provision "shell", inline: "echo Hello User"

  config.vm.define "ubuntu" do |ubuntu|
    ubuntu.vm.box = "ubuntu/xenial64"

    ubuntu.vm.network :private_network, virtualbox__intnet: "link1", ip: "10.1.1.10"
    ubuntu.vm.provision :shell, path: "scripts/ubuntu.sh", privileged: true
  end

  config.vm.define "xr" do |xr|
    xr.vm.box = "IOS-XRv"
    xr.vm.network :private_network, auto_config: false, virtualbox__intnet: "link1", ip: "10.1.1.20"
    xr.vm.provision "file", source: "configs/rtr_config", destination: "/home/vagrant/rtr_config"
    
    xr.vm.provision "shell" do |s|
      s.path =  "scripts/apply_config.sh"
      s.args = ["/home/vagrant/rtr_config"]
    end
  end    
end
