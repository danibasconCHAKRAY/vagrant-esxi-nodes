# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"


Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  (1..5).each do |i|
    config.vm.define "k8s-node#{i}" do |node|


  # set to false, if you do NOT want to check the correct VirtualBox Guest Additions version when booting this box
    if defined?(VagrantVbguest::Middleware)
      config.vbguest.auto_update = true
    end

    node.vm.box = "bento/ubuntu-16.04"
    node.vm.hostname = "k8s-worker#{i}"
    node.vm.synced_folder('.', '/Vagrantfiles', type: 'rsync')
    node.vm.network :forwarded_port, guest: 32280, host: 38080
    node.vm.network :forwarded_port, guest: 32443, host: 38443
    node.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"
  
    node.vm.provider "vmware_fusion" do |v, override|
       ## the puppetlabs ubuntu 14-04 image might work on vmware, not tested? 
      v.box = "bento/ubuntu-16.04"
      v.vmx["numvcpus"] = "2"
      v.vmx["memsize"] = "4096"
    end
    node.vm.provider :vmware_esxi do |esxi, overrider|
      #
      #   Provider settings
      #
      esxi.esxi_hostname = '10.10.1.10'
      esxi.esxi_username = 'vagrant'
      esxi.esxi_password = 'env:'
      esxi.esxi_virtual_network = 'VM Network'
      #esxi.esxi_hostport = 22
      #esxi.esxi_virtual_network = 'vmnet_example'
      #esxi.esxi_disk_store = 'DS_001'
      #esxi.esxi_resource_pool = '/Vagrant'
      esxi.guest_memsize = '4096'
      #esxi.guest_numvcpus = '2'
    end
    node.vm.provision :shell,
      :keep_color => true,
      :path => "setup.sh"
    end
  end
end
