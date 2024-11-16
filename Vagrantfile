# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "debian/bookworm64"
  config.vm.provision "shell", inline: <<-SHELL
  apt-get update
  apt-get install -y bind9 bind9-dnsutils
SHELL

  config.vm.define "dnsa" do |dnsa|
    dnsa.vm.network "private_network", ip: "192.168.57.103"
    dnsa.vm.provision "shell", name: "master-dns", inline: <<-SHELL

      cp /vagrant/named /etc/default/named
      cp /vagrant/named.conf.options /etc/bind/named.conf.options
      cp /vagrant/dnsa/named.conf.local /etc/bind/named.conf.local
      cp /vagrant/dnsa/ies.test /var/lib/bind/ies.test
      cp /vagrant/dnsa/57.168.192.rev /var/lib/bind/57.168.192.rev
 
    SHELL

  end
   

  config.vm.define "dnsb" do |dnsb|
    dnsb.vm.network "private_network", ip: "192.168.57.102"
    dnsb.vm.provision "shell", name: "slave-dns", inline: <<-SHELL

      cp /vagrant/named /etc/default/named
      cp /vagrant/named.conf.options /etc/bind/named.conf.options
      cp /vagrant/dnsb/named.conf.local /etc/bind/named.conf.local
 

    SHELL
  end
end

