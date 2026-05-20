# Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64"

  # Общие настройки для всех ВМ
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 1024
    vb.cpus = 1
  end

  # Узел 1
  config.vm.define "node1" do |node|
    node.vm.hostname = "node1"
    node.vm.network "private_network", ip: "192.168.56.11"
  end

  # Узел 2
  config.vm.define "node2" do |node|
    node.vm.hostname = "node2"
    node.vm.network "private_network", ip: "192.168.56.12"
  end

  # Провизия Ansible (запускается на каждой ВМ локально)
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "playbooks/site.yml"
    ansible.verbose = true
    ansible.install_mode = "default"  # установит Ansible на ВМ
    ansible.version = "latest"
    # Переменные, специфичные для каждой ВМ (можно вынести в отдельный файл)
    ansible.extra_vars = {
      target_host: "{{ inventory_hostname }}"
    }
  end
end