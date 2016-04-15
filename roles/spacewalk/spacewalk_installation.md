Spacewalk 2.x Installation notes
================================

https://fedorahosted.org/spacewalk/wiki/HowToInstall

Targetting CentOS 6.4

Environment Requirements
------------------------

###RAM

* 4GB Recommended
* 2GB Minimum

###Storage

* /var/satellite default package store.
* 6GB recommend by Red Hat.

Sum of:

* 250 KiB x number of clients
* 500 KiB x number of channels
* 230 KiB x number of packages in channel (1.1GiB for 5000 packages)

###Network

Details: https://access.redhat.com/site/solutions/10818

####Outbound

* TCP/80 HTTP
* TCP/443 HTTPS

**Optional**

* TCP/4545 Monitoring

####Inbound

* TCP/80 HTTP
* TCP/443 HTTPS

**Optional**

* TCP/5222 Push to clients
* TCP/5269 Push to Spacewalk Proxy
* UDP/69 TFTP

Installation
------------

###Repositories

**Spacewalk**

```sh
rpm -Uvh http://yum.spacewalkproject.org/2.0/RHEL/6/x86_64/spacewalk-repo-2.0-3.el6.noarch.rpm
```

**JPackage**
```ini
cat > /etc/yum.repos.d/jpackage.repo << EOF
[jpackage-generic]
name=JPackage generic
#baseurl=http://mirrors.dotsrc.org/pub/jpackage/5.0/generic/free/
mirrorlist=http://www.jpackage.org/mirrorlist.php?dist=generic&type=free&release=5.0
enabled=1
gpgcheck=1
gpgkey=http://www.jpackage.org/jpackage.asc
EOF
```

**EPEL**

```sh
rpm -Uvh http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
```

###Database

Using PostgreSQL only

####Spacewalk auto 

Runs on same server as spacewalk

```sh
yum install spacewalk-setup-postgresql
yum install spacewalk-postgresql 
```

####Postgres manual

https://fedorahosted.org/spacewalk/wiki/PostgreSQLServerSetup

###Application

**Answer file**
```ini
admin-email = root@localhost
ssl-set-org = Spacewalk Org
ssl-set-org-unit = spacewalk
ssl-set-city = My City
ssl-set-state = My State
ssl-set-country = US
ssl-password = spacewalk
ssl-set-email = root@localhost
ssl-config-sslvhost = Y
db-backend=postgresql
db-name=spaceschema
db-user=spaceuser
db-password=spacepw
db-host=host
db-port=5432
enable-tftp=Y
```

```sh
spacewalk-setup --disconnected --answer-file=<answer_file_name>
```


