# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define :openssh_ldap do |v|
    v.vm.hostname = "vagrant"
	v.vm.box = "ubuntu/trusty64"  # Ubuntu 14.04 Trusty
	#v.vm.box = "chef/centos-6.6" # CentOS 6
	#v.vm.box = "chef/centos-7.0" # CentOS7
    v.vm.network :private_network, ip: "192.168.100.20"
    v.vm.synced_folder ".", "/vagrant"
    v.vm.provider "virtualbox" do |v|
      v.customize ["modifyvm", :id, "--memory", 2048, "--cpus", 2]
      v.gui = false
    end
    v.vm.provision "ansible" do |ansible|
        ansible.sudo = true
        ansible.verbose = "vv"
        ansible.playbook = "site.yml"
        ansible.limit = "all"
    end
  end
end
