# kali-vagrant-ansible

A simple Vagrant script to launch a Kali virtual machine and prepare it for use via Ansible.

## Requirements
- MacOS
- VirtualBox
- Vagrant
- Ansible

Yes, this is currently written for my development environment. Future versions might be more system agnostic -- or they may not be. If you are familiar enough with Vagrant, only minor changes will be needed to make it work on Windows or Linux. Then again, if that is the case, you could probably write your own.

## Why?
I use Kali in a virtual machine on a regular basis, and I really dislike using mouse-clicks and repeated key-strokes to configure things. Vagrant captures all the standard configuration I use, and Ansible makes configuration of applications in Kali super easy. Having a fresh machine boot, update, and install needed packages with a simple command (`vagrant up`) is just cool, OK?

## TO-DO
1. Change openvas default configurations and move openvas config into its own Ansible role
2. Lock down bridged interface for scanning
3. Stop using default "vagrant" user and insecure keys
