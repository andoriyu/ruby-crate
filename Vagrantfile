require 'yaml'
Vagrant.configure('2') do |config|
  config.vm.box = 'precise32'
  config.vm.box_url = 'http://files.vagrantup.com/precise32.box'
  config.vm.hostname = 'ruby-crate'

  config.vm.provider :virtualbox do |vb|
    vb.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root", "1"]
  end
  works_file = 'works.yml'
  works = YAML::load_file(works_file) if File.exist?(works_file)
  works['shares'].each do |share|
    config.vm.synced_folder share['path'], "/works/#{share['name']}"
  end
  works['ports'].each do |port|
   config.vm.network :forwarded_port, guest: port, host: port
  end
    

  config.vm.provision :shell do |shell|
    shell.inline = "
      mkdir -p /etc/puppet/modules;
      puppet module install akumria/postgresql;
      puppet module install example42/redis;
      puppet module install maestrodev/rvm;
      puppet module install maestrodev/ant;
      puppet module install attachmentgenie/locales;
      "
  end
  config.vm.provision :puppet do |puppet|
    puppet.manifests_path = 'puppet/manifests'
  end
end
