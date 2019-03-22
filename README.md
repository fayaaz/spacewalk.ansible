Spacewalk playbooks and roles
==============

Changes:
- Updated to Spacewalk version 2.9
- Updated the iptables role
- Admin account is automatically created
- To enable a fully automated installation the password question has been removed.
- Default admin password is admin
- Default company name is Spacewalk
- The default information can be changed in this file: ./roles/spacewalk-customisations/defaults/main.yml
- Due to this ansible issue: https://github.com/ansible/ansible/issues/47210 the installation for spacewalk-postgresql does not use the yum module, due to a bug in the module they playbook will fail. Should be fixed when Ansible 2.8 is released.
- Added support for Ubuntu Bionic

Hardware / Virtual sizing advisement:
- 1 CPU, 4GB of ram minimum, 64GB of disk 

Todo:
- Add a lazy people script for: SpaceWalk proxy and client

For the lazy people: one command to install both ansible and run the spacewalk server installation playbook (requires you to be root):
```
sh <(curl -s https://raw.githubusercontent.com/rhessing/spacewalk.ansible/master/init.sh)
```


Install a full Spacewalk server on CentOS 7 and also adds customizations:
- CentOS 6 base+extras+epel+updates repos, channel and activation key 
- CentOS 7 base+extras+epel+updates repos, channel and activation key
- Ubuntu 18.06 base+security repos, channel and activation key (and repo sync scripts)
- Ubuntu 16.06 base+security repos, channel and activation key (and repo sync scripts)
- Ubuntu 14.04 base+security repos, channel and activation key (and repo sync scripts)
- Ubuntu 12.04 base+security repos, channel and activation key (and repo sync scripts)

Thanks to geerlingguy's iptables role, which is included here to configure the firewall on the server.

#### To do:

- Add Ubuntu support to client role (16.04 now working and tested)
- Look at also adding Debian Jessie/Wheezy

What my inventory (/etc/ansible/hosts) looks like:

```
[spacewalk-server]
spacewalk ansible_ssh_host=XXX.XXX.XXX.XXX

[spacewalk-clients]
Client01 ansible_ssh_host=XXX.XXX.XXX.XXX
Client02 ansible_ssh_host=XXX.XXX.XXX.XXX
```

### How to run:
#### Server:
```
ansible-playbook spacewalk.yml
```

The server initial setup will take a while to run - once this is done it will prompt you if you are ready.
At this point you should browse to the newly installed spacewalk instance in your browser and set up an admin username and password.
The prompt will ask for the password to continue.

#### Client:
```
ansible-playbook spacewalk-clients.yml
```

Extra credits:
Blog post: [Running Ubuntu Servers with Spacewalk](http://www.devops-blog.net/spacewalk/registering-ubuntu-and-debian-servers-with-spacewalk)
