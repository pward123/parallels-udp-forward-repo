# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "generic/ubuntu1804"
  config.vm.network "forwarded_port", guest: 14550, host: 14550, protocol: "udp"
  config.vm.provider "parallels" do |prl|
    prl.update_guest_tools = true
  end
end
