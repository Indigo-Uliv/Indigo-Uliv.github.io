# How to setup SSH Keys

## Introduction

Nodes are managed by a controlling machine (admin node) over SSH.
As a consequence, all nodes of the cluster should first be
configured to be accessible via SSH from the admin node.

Generating a key pair provides you with two long string of
characters, a public and a private key. The admin node will have
the private key and each node will need the public key. When the
two match up, the system unlocks without the need for a password.


## Create the RSA Key pair

The first step is to create the key pair on the admin node.

```
$ ssh-keygen -t RSA
```

## Copy the Public Key to Indigo nodes

Once the key pair is generated, you can place the public key on
each node you want to install, for the _**indigo**_ user. You can
copy the key in the authorized_keys file of the machine with the
_ssh-copy-id_ command.

```
$ ssh-copy-id indigo@192.168.12.12
```

Alternatively you can copy the public key from the file
_~/.ssh/id_rsa.pub_ on your admin node and paste it on the file
_~/.ssh/authorized_keys_ on the guest node.

```
$ mkdir -p ~/.ssh
$ chmod 700 ~/.ssh
$ nano ~/.ssh/authorized_keys"
$ chmod 600 ~/.ssh/authorized_keys
```
