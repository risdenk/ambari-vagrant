ambari-vagrant
==============

Vagrant setup for creating Ambari development/test virtual machines

Getting Started
---------------
### Install [Virtualbox](http://www.virtualbox.org/wiki/Downloads)
Download latest version of Virtual and install.

### Install [Vagrant](http://downloads.vagrantup.com)
Download latest version of Vagrant and install.

### Install Vagrant Plugins
Vagrant plugins increase the functionality of vagrant. They are installed by calling `vagrant plugin install PLUGINNAME`

The plugins to install are: vagrant-hostmanager, vagrant-librarian-chef

### Clone the Repo
1. `git clone https://github.com/risdenk/ambari-vagrant.git`
2. `cd ambari-vagrant`

### Boot the machine
The following steps will download the base VM if it does not exist, boot a single VM, and set the /etc/hosts file up with the correct hostnames.

1. `cd centos6.4`
2. `./up.sh 1` OR `vagrant up c6401`

### Install Ambari
Modified from the Testing Ambari section of https://cwiki.apache.org/confluence/display/AMBARI/Quick+Start+Guide

1. `vagrant ssh c6401`
2. `sudo su -`
3. `wget -O /etc/yum.repos.d/ambari.repo http://public-repo-1.hortonworks.com/ambari/centos6/1.x/GA/ambari.repo`
4. `yum install epel-release -y`
5. `yum install ambari-server -y`
6. `ambari-server setup`
7. `ambari-server start`

### Install the Cluster
1. Navigate to `http://c6401.vagrant:8080`
2. Login with username __admin__ and password __admin__
3. For the target host use the FQDN `c6401.vagrant`
4. Upload the __insecure\_private\_key__ from `~/.vagrant.d/insecure_private_key`
5. Specify __vagrant__ as the non-root SSH user
6. Follow the remaining steps

### If you get spammed by Nagios emails detailing warnings and critical failures
1. ssh into the server with `vagrant ssh c6401`.
2. Reboot the server with `sudo reboot`. This will kick you off ssh.
3. Wait for machine reboot. You can watch status on VirtualBox or ping the box with `ping c6401.vagrant` or ping the ip found from `cat /etc/hosts`.
4. Once it's back up, ssh again with `vagrant ssh c6401`.
5. Run `sudo ambari-server start` to get Ambari started again.
6. Navigate to `http://c6401.vagrant:8080` as normal.
