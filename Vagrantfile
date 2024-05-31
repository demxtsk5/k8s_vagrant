Vagrant.configure("2") do |config|

  start_ip_address = "192.168.56.101"
  num_vms = 3

  num_vms.times do |i|
    ip_address = "#{start_ip_address.split('.')[0..2].join('.')}.#{start_ip_address.split('.')[3].to_i + i}"

    config.vm.define "K3S-#{ip_address}" do |m|
      # generals
      m.vm.box = "ubuntu/jammy64"
      m.vm.boot_timeout = 300
      m.vm.hostname = "K3S-#{i+1}"

      # provider specification 
      m.vm.provider "virtualbox" do |v|
        v.name = "K3S (Ubuntu 22.04 LTS) - #{ip_address}"
        v.memory = 4000
        v.cpus = 2
      end

      # networking
      m.vm.network "private_network", type: "static", ip: ip_address
      m.vm.network "public_network"

      # synced folders
      m.vm.synced_folder ".", "/vagrant", disabled: false

      # provision
      if i == 0
        m.vm.provision "shell", inline: <<-SHELL
        sudo sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config
        sudo systemctl restart ssh
        # install k3s server
        curl -sfL https://get.k3s.io | sh -s - server --cluster-init --node-ip "#{ip_address}" --flannel-iface enp0s9 # defines bridge as flannel interface
        sudo cat /var/lib/rancher/k3s/server/node-token > /vagrant/node-token
        SHELL
      else
        m.vm.provision "shell", inline: <<-SHELL
        sudo sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config
        sudo systemctl restart ssh
        # install k3s agent
        node_token=$(cat /vagrant/node-token)
        curl -sfL https://get.k3s.io | sh -s - server --server "https://#{start_ip_address}:6443" --token $node_token --node-ip "#{ip_address}" --flannel-iface enp0s9 # defines bridge as flannel interface
        SHELL
      end
    end
  end
end
