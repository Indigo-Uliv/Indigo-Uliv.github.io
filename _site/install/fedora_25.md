# Fedora 25 server configuration


### Create a sudo user

Indigo expects a user named _**indigo**_ with sudo access

```
$ sudo adduser indigo
$ sudo adduser indigo sudo
```

### Configure hostname

It is useful for Cassandra to configure properly hostnames if you plan to
create a ring for the database

```
$ sudo hostname ring-1
$ sudo nano /etc/hostname
$ sudo nano /etc/hosts
```

### Configure network interface

On virtual machines it may be useful to use another network interface so the
web server on the server can be accessed from the host. This is the
configuration you can used to define a static IP (attached to the host-only
adapter in VirtualBox for instance)

```
$ sudo nano /etc/sysconfig/network-scripts/ifcfg-enp0s8
```

```
NAME=enp0s8
BOOTPROTO=static
ONBOOT=yes
IPADDR=192.168.56.111
NETMASK=255.255.255.0
BROADCAST=192.168.56.255
```

```
$ sudo ifdown enp0s8
$ sudo ifup enp0s8
```

### Configure ssh

See [SSH Configuration](ssh).

### Install Python 2.7

```
$ sudo yum install -y python27
$ sudo yum install -y python2-dnf
$ sudo yum install -y libselinux-python
$ sudo dnf install -y yum
```

### Download Oracle Java RPM (Temporary workaround)

Download it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
and put it in _indigo-deploy/roles/java/files_ in your admin node.


### Disable Firewall

```
$ sudo setenforce 0
$ sudo service firewalld stop
```
