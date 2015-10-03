VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "precise32"
  config.vm.box_url = "http://files.vagrantup.com/precise32.box"

    ## Machine 1
    config.vm.define :Machine_1 do |machine_1|
        machine_1.vm.network "public_network"
        machine_1.vm.network :forwarded_port, guest: 27018, host: 27018
        machine_1.vm.provider :vi do |v_1|
            v_1.name = "Machine_1"
        end
    end

    ## Machine 2
    config.vm.define :Machine_2 do |machine_2|
        machine_2.vm.network "public_network"
        machine_2.vm.network :forwarded_port, guest: 27019, host: 27019
        machine_2.vm.provider :virtualbox do |v_2|
            v_2.name = "Machine_2"
        end
    end
    ## Machine - Arbiter
    config.vm.define :Arbiter do |arbiter|
        arbiter.vm.network "public_network"
        arbiter.vm.network :forwarded_port, guest: 27020, host: 27020
        arbiter.vm.provider :virtualbox do |v_3|
            v_3.name = "test_vm3"
        end
    end

  config.vm.provision "ansible" do |ansible|
     ansible.playbook = "ansible_playbook/site.yml"
     ansible.verbose = "vvv"
  end

end
