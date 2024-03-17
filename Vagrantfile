require 'yaml'

Vagrant.configure("2") do |config|
  # Load and validate VM configurations from the YAML file
  begin
    inventory = YAML.load_file('boxes.yml')
  rescue Exception => e
    puts "Error loading YAML configuration: #{e.message}"
    exit 1
  end

  if inventory['vagrant'] && inventory['vagrant']['hosts']
    inventory['vagrant']['hosts'].each do |hostname, properties|
      # Define VM
      config.vm.define hostname do |cfg|
        cfg.vm.box = properties['v_box']
        cfg.vm.hostname = hostname
        cfg.vm.network :private_network, ip: properties['ansible_host']
        cfg.vm.network "forwarded_port", guest: 22, host: properties['v_exposed_ssh_port']

        # SSH key provisioning and permissions
        cfg.vm.provision "file", source: "files/id_vagrant", destination: "/home/vagrant/.ssh/id_rsa"
        cfg.vm.provision "file", source: "files/id_vagrant.pub", destination: "/home/vagrant/.ssh/id_rsa.pub"
        cfg.vm.provision "shell", inline: <<-SHELL
          chmod 600 /home/vagrant/.ssh/id_rsa /home/vagrant/.ssh/id_rsa.pub
          chmod 700 /home/vagrant/.ssh
          cat /home/vagrant/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys
          chmod 600 /home/vagrant/.ssh/authorized_keys
        SHELL


        # Common provisioning
        cfg.vm.provision "shell", inline: <<-SHELL
            echo "Running common provisioning tasks"
            apt-get update && apt-get upgrade -y
        #    if [ -f /var/run/reboot-required ]; then
        #      echo "Reboot required. Rebooting now..."
        #      /sbin/reboot
        #    else
        #      echo "No reboot required."
        #    fi
        SHELL

        config.trigger.after :provision do |trigger|
          trigger.name = "Checking for reboot requirement"
          trigger.run_remote = {inline: "if [ -f /var/tmp/reboot_required ]; then echo 'Rebooting now...' && /sbin/reboot; fi"}
        end

        # Provision apt packages
        if properties.key?('apt_packages') && !properties['apt_packages'].empty?
          apt_packages = properties['apt_packages'].join(' ')
          cfg.vm.provision "shell", inline: "sudo apt-get install -y #{apt_packages} && sudo apt autoremove -y"
        end

        # Controller-specific provisioning
        if properties['v_role'] == 'controller'
          cfg.vm.provision "shell", inline: "echo 'export ANSIBLE_CONFIG=/vagrant/ansible.cfg' >> /home/vagrant/.bash_profile", run: "always"
        end

        # Parallels provider customization
        cfg.vm.provider "parallels" do |prl|
          prl.name = hostname
          prl.memory = properties['v_mem']
          prl.cpus = properties['v_cpu']
          # Customize further if needed
        end
      end
    end
  else
    puts "Invalid or missing 'vagrant' or 'hosts' configurations in boxes.yml"
    exit 1
  end
end

