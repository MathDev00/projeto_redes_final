Vagrant.configure("2") do |config|

    config.vm.define "dhcp-server" do |dhcp|
      dhcp.vm.box = "ubuntu/bionic64"
      dhcp.vm.network "private_network", type: "dhcp"
      dhcp.vm.provision "shell", inline: <<-SHELL

      docker run -d --name dhcp-server -p 67:67/udp --cap-add=NET_ADMIN networkboot/dhcpd:edge
      SHELL
    end
  
    config.vm.define "dns-server" do |dns|
      dns.vm.box = "ubuntu/bionic64"
      dns.vm.network "private_network", type: "dhcp"
      dns.vm.provision "shell", inline: <<-SHELL

      docker run -d --name dns-server -p 53:53/udp --cap-add=NET_ADMIN networkboot/dnsmasq:edge
      SHELL
    end
  
    config.vm.define "web-server" do |web|
      web.vm.box = "ubuntu/bionic64"
      web.vm.network "forwarded_port", guest: 80, host: 8080
      web.vm.provision "shell", inline: <<-SHELL

      docker run -d --name web-server -p 80:80 nginx
      SHELL
    end
  
    config.vm.define "ftp-server" do |ftp|
      ftp.vm.box = "ubuntu/bionic64"
      ftp.vm.network "forwarded_port", guest: 21, host: 2121
      ftp.vm.provision "shell", inline: <<-SHELL
        docker run -d --name ftp-server -p 21:21 -v /path/to/ftp_data:/home/vsftpd/data fauria/vsftpd
      SHELL
    end
  
    config.vm.define "nfs-server" do |nfs|
      nfs.vm.box = "ubuntu/bionic64"
      nfs.vm.network "private_network", type: "dhcp"
      nfs.vm.provision "shell", inline: <<-SHELL

      docker run -d --name nfs-server --privileged -v /path/to/nfs_data:/exports -e SHARED_DIRECTORY=/exports -p 2049:2049 itsthenetwork/nfs-server-alpine:latest
      SHELL
    end
  
  end
  