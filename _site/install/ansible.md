# Deploy Indigo on a cluster using Ansible

## Introduction

[Ansible](https://www.ansible.com/) is a tool used to simplify the deployment of
Indigo on a cluster of machines (nodes). It is the preferred way to install and configure an Indigo cluster.

Nodes are managed by a controlling machine (admin node) over SSH. As a
consequence, all nodes of the cluster should first be configured to be accessible
via SSH from the admin node, used to deploy Indigo. By default it assumes you
are using SSH keys.

[ Note, if you intend to run multiple servers, know beforehand the details of
the networks, as it is best to set up the system with the 'real' network rather
than using localhost. ]


##  Pre-requesites

### Guest machines


* Ansible expects a user _**indigo**_ to exist with sudo rights.  

```
$ sudo adduser  indigo
$ sudo usermod -G sudo,adm indigo
```

* Make sure you have access to the guest node via [SSH](ssh)

### Admin node

* Install Ansible and GIT on the admin node (host) from which you
are deploying your cluster.

```
$ sudo apt install software-properties-common
$ sudo apt-add-repository ppa:ansible/ansible
$ sudo apt-get update
$ sudo apt install ansible git
```

* Clone the [indigo-deploy](https://github.com/Indigo-Uliv/indigo-deploy)
repository

```
$ git clone https://github.com/Indigo-Uliv/indigo-deploy.git
$ cd indigo-deploy
```

## Ansible Configuration

* By default the user account on the server should be 'indigo' who should have
sudo access. If different, you can modify the _**install_user**_ variable in the
file _./inventory/group_vars_.

* Cassandra stores its data in /var/lib/cassandra by default. This may be
redirected to an appropriate storage volume on the nodes, either via a symbolic
link or using something like:

```
$ mkdir /var/lib/cassandra
$ mount --bind <target> /var/lib/cassandra
$ mkdir /var/lib/cassandra/data
# Ensure that permissions and ownership are appropriately set
$ chown -R casssandra:cassandra /var/lib/cassandra
```

* Create a ```hosts``` file containing the IP address of the servers. You can
find an example in _./inventory/staging_

```
[cassandra_nodes]
indigo-node01 node_ip=192.168.56.110 seed=true
#indigo-node02 node_ip=192.168.56.111 seed=true

[all_cassandra_nodes:children]
cassandra_nodes

[indigo-webservers]
indigo-node01
#indigo-node02

```

* The cassandra_nodes part defines the machines that will form the cassandra
cluster. The IP address is the one which is used by Cassandra to communicate.
The nodes marked as seeds will be used in the Cassandra configuration file to
set up the seeds of the cluster.

* The indigo-webservers part defines where the indigo-web server will be running.

* The default behavior for the web server is to use HTTP. If needed this can be changed in the indigo.yml file with the variable https_mode. The nginx server is using the SSL certificate in /etc/nginx/ssl/nginx.crt. If they are not present a self-signed version is created during deployment.

* The deployment is configured to use systemd by default. If you need to use
upstart there's a script that can be used and deployed during install. This is
commented in the main.yml task for indigo-web and indigo-listener role.


## Deploying

Run the deployment with the following command:

```
ansible-playbook full.yml -i inventory/staging --ask-become-pass
```
