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
  # Creates a VM named 'kali', with 4GB RAM and 1 vCPU
  config.vm.provider "virtualbox" do |vb|
    vb.name = "kali"
    vb.gui = false
    vb.memory = 4096
    vb.cpus = 1
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  # Network configuration
  config.vm.hostname = "PRINTER-X5423.456.n0"
  config.vm.network "public_network", bridge: 'en0: Ethernet'
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
