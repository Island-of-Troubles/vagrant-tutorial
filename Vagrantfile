# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp-education/ubuntu-24-04"
  config.vm.box_version = "0.1.0"

  # Install Docker and dependencies
  config.vm.provision "shell", name: "install-dependencies", path: "install-dependencies.sh"

  # Start Terramino (can be rerun with vagrant provision --provision-with start-terramino)
  config.vm.provision "shell", name: "start-terramino", inline: <<-SHELL
    cd /home/vagrant/terramino-go
    docker compose up -d
  SHELL

  # Restart Terramino (can be rerun with vagrant provision --provision-with restart-terramino)
  # For quick changes that doesn't require rebuilding (e.g. frontend changes)
  config.vm.provision "shell", name: "restart-terramino", run: "never", inline: <<-SHELL
    docker compose restart
  SHELL

  # Reload Terramino (can be rerun with vagrant provision --provision-with reload-terramino)
  # For changes that require rebuilding (e.g. backend changes)
  config.vm.provision "shell", name: "reload-terramino", run: "never", inline: <<-SHELL
    /usr/local/bin/reload-terramino
  SHELL

  # Forward ports for Terramino (8081 for frontend, 8080 for backend)
  config.vm.network "forwarded_port", guest: 8080, host: 8080
  config.vm.network "forwarded_port", guest: 8081, host: 8081

end
