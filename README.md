# vagrant-tutorial
Vagrant is a CLI utility for managing virtual machines.
It connects to a provider (e.g. VirtualBox, AWS) to provision and configure reproducible development environments using a simple `Vagrantfile` (similar to a `Dockerfile` or `docker-compose.yml`).

## Basic concepts

- **Box**: a base image used to create the virtual machine. Boxes are reusable, shareable, and versioned. You can find public boxes on [Vagrant Cloud](https://app.vagrantup.com/boxes/search).
- **Provider**: the underlying system that runs the VM. Common providers are VirtualBox, VMware, and Docker.
- **Provisioning**: the process of setting up the VM after it's created. You can install packages, run scripts, or configure services.
- **Provisioner**: the tool used to provision the VM. Vagrant supports several, including Shell, Ansible, Puppet, and Chef.
- **Synced folders**: a way to share files between your host machine and the VM. By default, the project folder is mounted inside the VM.

## Main commands

- `vagrant init hashicorp-education/ubuntu-24-04 --box-version 0.1.0` - creates a basic Vagrantfile
- `vagrant up` - starts the VM (downloads box if needed; default provider is VirtualBox)
- `vagrant ssh` - connects to the VM via SSH
- `vagrant suspend` - pauses the VM and saves its state to disk
- `vagrant resume` - resumes a suspended VM
- `vagrant halt` - shuts down the VM gracefully
- `vagrant destroy` - deletes the VM and associated resources
- `vagrant box remove hashicorp-education/ubuntu-24-04` - removes the specified box from your system
- `vagrant provision` - runs the provisioners again without restarting the VM
- `vagrant up --provision` - starts the VM and runs provisioners
- `vagrant reload` - restarts the VM and reloads the Vagrantfile configuration
- `vagrant reload --provision` - restarts the VM and re-applies provisioners
- `vagrant provision --provision-with <name>` - runs only the named provisioner(s), as defined in the Vagrantfile

## Example Vagrantfile
```ruby
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.network "forwarded_port", guest: 80, host: 8080
end
```

## Useful links
- https://developer.hashicorp.com/vagrant
- https://app.vagrantup.com/boxes/search
