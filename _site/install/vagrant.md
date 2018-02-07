# Vagrant configuration

Indigo provides a set of configuration files for [Vagrant] (https://www.vagrantup.com/) that can be used to quickly provision a
machine or a cluster to experiment with the system. These are some examples that can be used to start ubuntu or fedora machines.

## Ubuntu 16.04

* _Vagrantfile_

```
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.define "node0" do |node0|
    node0.vm.box = "hashicorp/precise64"
    node0.vm.box_version = "1.1.0"
    node0.vm.network "private_network", ip: "192.168.12.10"

    node0.vm.provider "virtualbox" do |v|
       v.memory = "1024"
    end
  end
end
```

## Fedora 27

* _Vagrantfile_

```
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.define "node0" do |node0|
    indigo.vm.box = "generic/fedora27"
    node0.vm.network "private_network", ip: "192.168.12.11"

    node0.vm.provider "virtualbox" do |v|
       v.memory = "1024"
    end
  end
end
```



## Usage

### Create and provision the box

```
$ vagrant up
```

### Log to the box

```
$ vagrant ssh
```

### Troubleshooting

If there's an error for the install of the virtualbox guest additions you can try
a manual install. vbguest is useful to share folders to the box.

```
$ vagrant up
$ vagrant vbguest --do install --no-cleanup
```

Then in the box

```
$vagrant ssh
```

Run the installer manually

```
$ sudo /mnt/VBoxLinuxAdditions.run
```
