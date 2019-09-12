# -*- mode: ruby -*-
# vi: set ft=ruby :

local_project_dir = File.absolute_path(".")
project_dir = "/var/www/development/"
project_name = File.basename(project_dir)

$script = <<-SCRIPT
echo Fetching the Vagrant local ip
vagrant ssh -c "hostname -I | cut -d' ' -f2" 2>/dev/null > inventory/hosts
SCRIPT

Vagrant.configure("2") do |config|

  config.vm.define :dev do |dev|
    dev.vm.box = "geerlingguy/ubuntu1804"
    dev.vm.hostname = "test"

    dev.vm.network "forwarded_port", guest: 80, host: 8080
    dev.vm.network "private_network", type: "dhcp"

    dev.vm.synced_folder ".", "/vagrant", disabled: true
    dev.vm.provision :shell, :inline => "mkdir -p " + project_dir

    dev.vm.synced_folder local_project_dir + "/Projects", project_dir, type: "nfs"

    dev.vm.define project_name do |node|
        node.vm.host_name = project_name + ".local.michel-pouwels.nl"
    end

    dev.vm.provision :shell, :inline => "sudo apt install net-tools", run: "always"
    dev.vm.provision :shell, :inline => "sudo rm /etc/localtime", run: "always"
    dev.vm.provision :shell, :inline => "sudo ln -s /usr/share/zoneinfo/Europe/Amsterdam /etc/localtime", run: "always"

  end
  # config.vm.define :accept do |accept|
  #   psstep.vm.box = "geerlingguy/ubuntu1804"
  #   psstep.vm.network "public_network", :bridge => 'en0: Ethernet'
  #   psstep.vm.hostname = "acceptance"
  # end
  # config.vm.define :prod do |prod|
  #   psprod.vm.box = "geerlingguy/ubuntu1804"
  #   psprod.vm.network "public_network", :bridge => 'en0: Ethernet'
  #   psprod.vm.hostname = "production"
  # end

end