# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "ubuntu/trusty64"
  # config.vm.box_url = myconf['box_url']

  # myconf['synced_folders'].each do |sf|
  #   config.vm.synced_folder sf['src'], sf['dest'], sf['type'] => { :mount_options => sf['options'] }
  # end

  config.vm.define :jenkins1 do |cfg|
    cfg.vm.hostname = 'jenkins1'

    # cfg.vm.network :forwarded_port, guest:5432, host:9432
    cfg.vm.network :private_network, ip: "192.168.33.28"

    cfg.vm.provider "virtualbox" do |v|
        v.customize ["modifyvm", :id, "--memory", 1024]
        v.customize ["modifyvm", :id, "--cpus", 1]
    end
  end

  config.vm.provision :ansible do |ansible|
    ansible.limit = 'all'
    ansible.playbook = "ansible/site.yml"
    ansible.inventory_path = "ansible/inventories/mystack"
    ansible.verbose = 'vvvv'
  end
end
