Vagrant.configure("2") do |config|
  config.vm.box = "monero"
  config.vm.hostname = "ubuntu-vagrant"
  config.ssh.username = "ubuntu"
  # Ignore vguest updates during prov (faster)
  config.vbguest.auto_update = false
  config.vm.synced_folder "storage/", "/vagrant/storage", create: true
  
config.vm.provider "virtualbox" do |v|   
  v.memory = 2048   
  v.cpus = 4
  # prevents Stderr: VBoxManage.exe: error: RawFile#0 failed to create the raw output file
  v.customize [ "modifyvm", :id, "--uartmode1", "disconnected" ]
end

  # -= ANSIBLE =-
  # Use :ansible or :ansible_local to provision
  config.vm.provision :ansible_local do |ansible|
    ansible.playbook = "provisioning/site.yml"
    ansible.install_mode = "pip"
    ansible.version = "2.4.2.0"
  end
end
