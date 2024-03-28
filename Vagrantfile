VAGRANTFILE_API_VERSION = "2"
ENV['VAGRANT_DEFAULT_PROVIDER'] = 'libvirt'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  ### global configs
  config.ssh.insert_key = false # important

  config.vm.define "sambadc" do |host|
    host.vm.hostname = "sambadc"
    host.vm.box = "debian/bookworm64"
    host.vm.network :private_network,
      :ip => "192.168.40.2",
      :libvirt__network_name => "uspdev",
      :libvirt__forward_mode => "nat"
    host.vm.provider :libvirt do |v|
      v.memory = 1024
      v.cpus = 1
    end
  end
    
  config.vm.define "clientedeb" do |host|
    host.vm.hostname = "clientedeb"
    host.vm.box = "debian/bookworm64"
    host.vm.network :private_network,
      :ip => "192.168.40.3",
      :libvirt__network_name => "uspdev",
      :libvirt__forward_mode => "nat"
    host.vm.provider :libvirt do |v|
      v.memory = 4096
      v.cpus = 4
    end
  end

  config.vm.define "cups" do |host|
    host.vm.hostname = "cups"
    host.vm.box = "debian/bookworm64"
    host.vm.network :private_network,
      :ip => "192.168.40.4",
      :libvirt__network_name => "uspdev",
      :libvirt__forward_mode => "nat"
    host.vm.provider :libvirt do |v|
      v.memory = 1024
      v.cpus = 1
    end
  end
end
