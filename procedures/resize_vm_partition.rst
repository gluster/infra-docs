Resizing a partition in a VM
============================

VMs installed by our automation role will use a LVM backed storage, permitting
easier resizing. The process is not automated yet, partially because this is
unfrequent enough to not warrant automation right now.

This can be done online if LVM is used all the way, which is the case right now.

Step 1: Resize the logical volume on the hypervisor
---------------------------------------------------

On the hypervisor (host.example.org), we have to resize the logical volume.
Each VM has 2 differents volume, one for the system, one for the data. System is supposed
to be wiped on reinstall, and data is not. Let's assume we are resizing the data volume, 
and adding 50 G to a 100G disk. This operation have to happen on the hypervisor, for
a VM called vm.example.org::

    lvextend -L 150G /dev/mapper/host-guest--vm.example.org_data

Step 2: Ask to QEMU to refresh the disk
---------------------------------------

The operation need the size of the block device, so we need to reuse it::

    virsh blockresize vm.example.org /dev/mapper/host-guest--vm.example.org_data 150G 

Step 3: Resize the disk in the VM
---------------------------------

First, we have to resize the physical volume on vm.example.org. The data partition is usually
on /dev/vdb but it depend on the VM. The command pvresize is safe to run in all case::

    pvresize -v /dev/vdb

Then the volume need to be resized, either to take 100% of the space or more, using -L::

    lvresize /dev/mapper/guest-data

And finally, grow the filesystem. This step depend on the filesystem used. For
example, for xfs, the command would be::

    xfs_growth /dev/mapper/guest-data

For ext4, it would be::

    resize_e2fs /dev/mapper/guest-data

Step 4: reflect the change in the playbook
------------------------------------------

If any change is done, it should be reflected in the playbook. There
is usually something to change on the hypervisor playbook, and depending
on the VM, in the playbook to deploy the VM or any filesystem deployed there.
