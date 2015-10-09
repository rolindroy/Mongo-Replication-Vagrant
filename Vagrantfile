VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "precise32"
  config.vm.box_url = "http://files.vagrantup.com/precise32.box"

    base_dir = File.expand_path(File.dirname(__FILE__))
    
    cluster = {
        "mongo1"   => { :ip => "192.168.100.153"},
        "mongo2"   => { :ip => "192.168.100.161"},
        "mongo3"   => { :ip => "192.168.100.157"},
        "arbitor"  => { :ip => "192.168.100.154"},
    }

    cluster.each_with_index do |(hostname, info), index|
        config.vm.define hostname do |cfg|

          cfg.vm.provider :virtualbox do |vb, override|
            override.vm.network :public_network, ip: "#{info[:ip]}"
            override.vm.hostname = hostname
            vb.name = 'vagrant-' + hostname
          end
        end 
    end

  config.vm.provision "ansible" do |ansible|
     ansible.playbook = "ansible_playbook/site.yml"
     ansible.inventory_path = "hosts"
  end

end
