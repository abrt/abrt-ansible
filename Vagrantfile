Vagrant.configure("2") do |config|
  config.vm.define "faf" do |faf|
    faf.vm.box = "fedora/30-cloud-base"
    faf.vm.hostname = "faf.local"
    faf.vm.provider :libvirt do |domain|
      domain.memory = 2048
      domain.cpus = 2
      domain.volume_cache = 'none'
      domain.driver = "kvm"
      domain.storage_pool_name = "default"
    end

    faf.vm.provision "ansible" do |ansible|
       ansible.playbook = "site.yml"
       ansible.become = true
       ansible.config_file = "conf/ansible.cfg"
       ansible.compatibility_mode = "auto"
       ansible.groups = {
         "faf" => ["faf"],
         "all_groups:children" => ["faf"]
       }

       ansible.extra_vars = {
          faf_first_time_setup: true,
       }
    end
  end

  config.vm.define "rs" do |rs|
    rs.vm.box = "fedora/30-cloud-base"
    rs.vm.hostname = "rs.local"
    rs.vm.provider :libvirt do |domain|
      domain.memory = 2048
      domain.cpus = 2
      domain.volume_cache = 'none'
      domain.driver = "kvm"
      domain.storage_pool_name = "default"
    end

    rs.vm.provision "ansible" do |ansible|
       ansible.playbook = "site.yml"
       ansible.become = true
       ansible.config_file = "conf/ansible.cfg"
       ansible.compatibility_mode = "auto"
       ansible.groups = {
         "retrace_server" => ["rs"],
         "all_groups:children" => ["rs"]
       }
       ansible.extra_vars = {
         selinux: true,
       }
     end
  end

  config.vm.synced_folder ".", "/mnt", disabled: true
end
