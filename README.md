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
- Added support for Ubuntu Bionic

Hardware / Virtual sizing advisement:
- 1 CPU, 4GB of ram minimum, 64GB of disk 



For the lazy people: 
To install both ansible and the spacewalk server:
```
sh <(curl -s https://raw.githubusercontent.com/rhessing/spacewalk.ansible/master/init-server.sh)
```

To install both ansible and the spacewalk proxy:
```
sh <(curl -s https://raw.githubusercontent.com/rhessing/spacewalk.ansible/master/init-proxy.sh)
```

To install both ansible and the spacewalk client:
```
sh <(curl -s https://raw.githubusercontent.com/rhessing/spacewalk.ansible/master/init-client.sh)
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

- Check Ubuntu support to client role on versions 12.04, 14.04, 16.04 and 18.04
- Add a lazy people script for: SpaceWalk proxy and client

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
