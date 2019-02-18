# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "bento/debian-9.6"

  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = true
  
    # Customize the amount of memory on the VM:
    vb.memory = "1024"
    vb.customize ["modifyvm", :id, "--vram", "128"]

    # Shared folder
    config.vm.synced_folder ".", "/vagrant", automount: true

    # Expose the gemini PDA usb to the VM
    vb.customize ["modifyvm", :id, "--usb", "on"]
    vb.customize ["modifyvm", :id, "--usbehci", "on"]
    vb.customize ["usbfilter", "add", "0", 
      "--target", :id, 
      "--name", "Gemini PDA",
      "--vendorid", "0e8d"]
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt update
    apt upgrade -y
    apt install -y gnome-shell gnome-terminal libaudio2
    update-rc.d gdm3 enable
    service gdm3 start
  SHELL
end
