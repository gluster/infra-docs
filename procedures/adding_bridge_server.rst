Adding a bridge on a hypervisor
-------------------------------

Current nmcli ansible module (as of Ansible 2.4) do not work work and
do not implement any bridge support, and fixing it would requires a rather
complete rewrite.

So we can't really automate this part.

Step 1: Creating the bridge with nmcli
======================================

Assuming we want to add a bridge `virbr2` to be used
for hypervisors, with a specific vlan connected on `em2`.

The following commands can be used::

    $ nmcli con add type bridge con-name virbr2 ifname virbr2
    $ nmcli con add type ethernet con-name em2 ifname em2 master virbr2
    $ nmcli con modify virbr2 bridge.stp no

Step 2: Complete the ansible configuration
==========================================

In order to not hardcode any interface, we use variable for each bridge connected
on a specific VLAN. They are meant to be used by the role that install VMs.

See the file network_interfaces.yml in each hypervisor host_vars directory in the ansible repository
for the format used.
 
