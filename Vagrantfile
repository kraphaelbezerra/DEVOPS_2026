Vagrant.configure("2") do |config|

  config.vm.provision "shell", path: "script.sh"

  # Configurações comuns a todas as VMs
  config.vm.box = "shekeriev/debian-11"
  config.vm.box_check_update = false
  
  # Configuração de recursos padrão
  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "1024"
    vb.cpus = 1
  end

  # VM Controle
  config.vm.define "controle" do |controle|
    controle.vm.hostname = "controle"
    controle.vm.network "private_network", ip: "172.17.177.100"
    controle.vm.provider "virtualbox" do |vb|
      vb.name = "controle"
    end
    controle.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.install_mode = "pip"
    end
  end

  # VM Web
  config.vm.define "web" do |web|
    web.vm.hostname = "web"
    web.vm.network "private_network", ip: "172.17.177.101"
    web.vm.provider "virtualbox" do |vb|
      vb.name = "web"
    end
  end

  # VM Banco de Dados
  config.vm.define "bd" do |bd|
    bd.vm.hostname = "bd"
    bd.vm.network "private_network", ip: "172.17.177.102"
    bd.disksize.size = '20G'
    bd.vm.provider "virtualbox" do |vb|
      vb.name = "bd"
    end
  end

  # Opcional: Provisionamento básico (descomente se necessário)
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get upgrade -y
  # SHELL

end