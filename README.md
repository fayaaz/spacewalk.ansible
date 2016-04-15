Spacewalk playbooks and roles
==============

Install a full Spacewalk server on CentOS 7 and also adds customizations:
- CentOS 6 repo, channel and activation key (+epel)
- CentOS 7 repo, channel and activation key(+epel)
- Ubuntu 14.04 repo, channel and activation key (and repo sync scripts)
- Ubuntu 12.04 repo, channel and activation key (and repo sync scripts)

Thanks to geerlingguy's iptables role, which is included here to configure the firewall on the server.

####To do:

- Add ubuntu support to client role
- Update client role to automatically pick EPEL for activation key
- Look at also adding Debian Jessie/Wheezy

What /etc/ansible/hosts looks like:

```
[spacewalk-server]
spacewalk ansible_ssh_host=XXX.XXX.XXX.XXX

[spacewalk-clients]
Client01 ansible_ssh_host=XXX.XXX.XXX.XXX
Client02 ansible_ssh_host=XXX.XXX.XXX.XXX
```

###How to run:
####Server:
```
ansible-playbook spacewalk.yml
```

The server initial setup will take a while to run - once this is done it will prompt you if you are ready.
At this point you should browse to the newly installed spacewalk instance in your browser and set up an admin username and password.
The prompt will ask for the password to continue.

####Client:
```
ansible-playbook spacewalk-clients.yml
```