# -*- mode: ruby -*-
# vi: set ft=ruby :

# List ports to map
ports = [9392, 9583, 9570, 9596]

Vagrant.configure("2") do |config|
  # Base VM OS configuration
  config.vm.box = "kalilinux/rolling"
  config.ssh.insert_key = false
  config.vm.synced_folder '.', '/vagrant', disabled: true

  # General VirtualBox VM configuration
  # Creates a VM named 'kali', with 1GB RAM and 1 vCPU
  config.vm.provider "virtualbox" do |vb|
    vb.name = "kali"
    vb.gui = false
    vb.memory = 1024
    vb.cpus = 1
    vb.check_guest_additions = true
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--ioapic", "on"]
    vb.customize ["modifyvm", :id, "--usb", "on"]
    vb.customize ["modifyvm", :id, "--usbehci", "on"]
# This is a filter for a Realtek RTL8812AU USB WiFi Adapter
    vb.customize ["usbfilter", 'add', '0', '--target', :id, '--name', 'USBWiFi', '--vendorid', '0x0bda', '--productid', '0x8812']
  end

  # Network configuration
  config.vm.hostname = "PRINTER-X5423.456.n0"
# this is a macOS interface and a Linux interface
  config.vm.network "public_network", bridge: [
    "en0: Ethernet",
    "enp0s25"
  ]
  ports.each do |port|
    config.vm.network "forwarded_port", guest: port, host: port
  end

  # Provision VM via Ansible
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/main.yml"
    ansible.compatibility_mode = "2.0"
    ansible.extra_vars = {
      ansible_python_interpreter: "/usr/bin/python3",
      ansible_user: 'vagrant',
      ansible_ssh_private_key_file: "~/.vagrant.d/insecure_private_key"
    }
  end
end
