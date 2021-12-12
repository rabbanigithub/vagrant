DISK_2 = "disk-2.vdi"
Vagrant.configure(2) do |config|
  config.ssh.insert_key = false
  config.vm.define "test" do |node|
    node.vm.box = "ubuntu/bionic64"
    node.vm.hostname = "jenkins"
    node.vm.network "private_network", ip: "10.11.12.100"
    node.vm.synced_folder '.', '/vagrant', disabled: true
    node.vm.provider "virtualbox" do |vb|
      vb.name = "ubuntu-16_04-1"
      vb.memory = 512
      if not File.exists?(DISK_2)
        vb.customize ['createhd', '--filename', DISK_2, '--size', 10 * 1024]
      end
      vb.customize [ 'storageattach', :id, '--storagectl', 'SCSI', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', File.absolute_path(DISK_2)]
    end
  end
end
