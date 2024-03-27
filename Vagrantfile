VAGRANTFILE_API_VERSION = "2"
ENV['VAGRANT_DEFAULT_PROVIDER'] = 'libvirt'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  ### global configs
  config.ssh.insert_key = false # important

  config.vm.define "sambadc" do |host|
    host.vm.hostname = "sambadc"
    host.vm.box = "generic/debian12"
    host.vm.network :private_network,
      :ip => "192.168.40.2",
      :libvirt__network_name => "fflch",
      :libvirt__forward_mode => "nat"
    host.vm.provider :libvirt do |v|
      v.memory = 1024
      v.cpus = 1
    end
  end

end
