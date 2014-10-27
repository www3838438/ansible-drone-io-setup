Ansible Drone setup
=========

## Whats inside
All the provisioning script is located in `provisioning/` folder. The script setups latest docker available from ubuntu repositories, installs mysql, docker, drone with mysql and gitlab authentication.

### Requirements
  - Ansible (tested with 1.7.1)
  - An ubuntu box, tested with 14.04 64bit

### Testing requirements
  - vagrant and virtualbox

### Configuration

Before running any of the playbook you should configure params in `provisioning/group_vars/all` file.

Second step is to create your inventory file, which should contain target host. The connection to the host should be made with a sudo user, not root.

### Basic usage:

`ansible-playbook -i provisioning/<inventory_file> playbook.yml`

Testing the playbook against vagrant box:

`ansible-playbook -i provisioning/testing playbook.yml`

In testing mode after the playbook finishes then navigate to http://10.0.0.111/ (see `VagrantFile`) to start using

### Useful links
 - [Docker](http://docker.com)
 - [Drone](http://github.com/drone/drone)
 - [Ansible](http://ansible.com)
 - [Vagrant](http://vagrantup.com)
