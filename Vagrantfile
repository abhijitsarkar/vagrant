# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"
Vagrant.require_version ">= 1.7.0"

$setup = <<SCRIPT
  # http://foo-o-rama.com/vagrant--stdin-is-not-a-tty--fix.html
  sed -i '/tty/!s/mesg n/tty -s \\&\\& mesg n/' /root/.profile
SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.hostname = "vagrant-" + "#{`hostname`[0..-2]}".sub(/\..*$/,'').downcase
  config.vm.provision "shell", inline: $setup
  config.vm.provision "docker"
  config.vm.network :forwarded_port, guest: 8080, host: 8080
  config.vm.synced_folder ".", "/vagrant", disabled: true
end