Vagrant.configure("2") do |config|
  config.vm.box = "generic/rhel8"
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "vagrant-playbook.yaml"
  end
end
