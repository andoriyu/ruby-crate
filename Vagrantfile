Vagrant.configure('2') do |config|
  config.vm.box = 'precise32'
  config.vm.box_url = 'http://files.vagrantup.com/precise32.box'
  config.vm.hostname = 'ruby-crate'

  config.vm.network :forwarded_port, guest: 3000, host: 3000

  config.vm.provision :shell do |shell|
    shell.inline = "
      mkdir -p /etc/puppet/modules;
      puppet module install akumria/postgresql;
      puppet module install example42/redis;
      "
  end
  config.vm.provision :puppet do |puppet|
    puppet.manifests_path = 'puppet/manifests'
  end
end
