# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.vm.box = "base"
    config.vm.box_url = "http://cloud-images.ubuntu.com/vagrant/raring/current/raring-server-cloudimg-amd64-vagrant-disk1.box"
    config.vm.network :private_network, ip: "192.168.12.34"
    config.vm.provider :virtualbox do |vb|
        vb.name = "ubuntu"
        vb.customize ["modifyvm", :id, "--memory", "2048"]
    end
    config.berkshelf.enabled = true
    config.omnibus.chef_version = :latest
    config.vm.provision "chef_solo" do |chef|
        chef.json = {
            :mysql => {
            :server_root_password => 'rootpass',
            :server_debian_password => 'debpass',
            :server_repl_password => 'replpass'
        }
        }
        #chef.add_recipe "apt"
        #chef.add_recipe "nginx"
        #chef.add_recipe "mysql"
        chef.run_list = ["recipe[apt::default]", "recipe[nginx::default]", "recipe[mysql::client]", "recipe[mysql::server]"]
    end
end
