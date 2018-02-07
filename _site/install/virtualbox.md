# VirtualBox Configuration

If you want to experiment on a local virtual machine (VM) using virtualbox for
instance, this is the usual configuration I'm using:

* Create a Host-ony Network in the VirtualBox settings (vboxnet0)
   * IPv4 address 192.168.56.1
* Basic configuration with enough memory, 1 hard disk
* Adapter 1 attached to NAT
* Adapter 2 attached to Host-only adapter (vboxnet0) so Host and Guest can see
each other on the 192.168.56.x network.
