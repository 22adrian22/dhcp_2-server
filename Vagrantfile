Vagrant.configure("2") do |config|

  # General

  config.vm.box = "debian/bookworm64"
  
  config.vm.provision "update", type: "shell",
                      inline: "apt-get update"
  
  # DHCP server
  
  config.vm.define "servidor" do |dhcp|
    
    dhcp.vm.network "private_network",
                    ip: "192.168.59.10"
    
    dhcp.vm.network "private_network",
                    ip: "192.168.10.1",
                    virtualbox__intnet: "intnet1"
    
    dhcp.vm.network "private_network",
                    ip: "192.168.20.1",
                    virtualbox__intnet: "intnet2"
                   
    
    dhcp.vm.provision "install", type: "shell",
                      inline: "apt-get install -y isc-dhcp-server"

    dhcp.vm.provision "config", type: "shell", inline: <<-SHELL
          sudo cp -v /vagrant/dhcpd.conf /etc/dhcp/dhcpd.conf
          sudo cp -v /vagrant/isc-dhcp-server /etc/default/isc-dhcp-server
          sudo systemctl start isc-dhcp-server                      
    SHELL
  end
  
  # DHCP client
  
  config.vm.define "PC-10" do |c1|
    
    c1.vm.network "private_network",
                  type: "dhcp",
                  virtualbox__intnet: "intnet1",
                  :mac => "001AA0E8C239"
    
  end
  config.vm.define "PC-11" do |c2|
    
    c2.vm.network "private_network",
                  type: "dhcp",
                  virtualbox__intnet: "intnet1",
                  :mac => "001AA0E6094A"
    
  end
  config.vm.define "PC-12" do |c3|
    
    c3.vm.network "private_network",
                  type: "dhcp",
                  virtualbox__intnet: "intnet1"
    
  end
  config.vm.define "PC-13" do |c4|
    
    c4.vm.network "private_network",
                  type: "dhcp",
                  virtualbox__intnet: "intnet2",
                  :mac => "001AA0E5F5D2"
    
  end
  config.vm.define "PC-14" do |c5|
    
    c5.vm.network "private_network",
                  type: "dhcp",
                  virtualbox__intnet: "intnet2",
                  :mac => "001AA0E906CF"
    
  end
  config.vm.define "PC-15" do |c6|
    
    c6.vm.network "private_network",
                  type: "dhcp",
                  virtualbox__intnet: "intnet2"
    end
end