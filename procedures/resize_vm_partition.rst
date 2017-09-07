Resizing a partition in a VM
============================

VM installed by our automation role will use a LVM backed storage, permitting
easier resizing. The process is not automated yet, partially because this is
unfrequent enough to not warrant automation right now.

Step 1: Stop the VM
-------------------

We found out that we can't resizing the VM online with the current setup. So it
has to be stop from virsh, or virt-manager.

First, stop the VM (guest-vm.example.org in this case)::

    halt

Then, on the hypervisor (host.example.org in this case)::

    virsh destroy guest-vm.example.org

Step 2: Resize the logical volume
---------------------------------

On the hypervisor (host.example.org), we have to resize the logical volume.
Each VM has 2 differents volume, one for the system, one for the data. System is supposed
to be wiped on reinstall, and data is not. Let's assume we are resizing the data volume, 
and adding 50 G. This operation have to happen on the hypervisor::

    lvextend -L +50G /dev/mapper/host-guest--vm.example.org_data

Step 3: Restart the VM and resize from inside
---------------------------------------------

Next step is to restart the VM. This can be done with virsh::

    virsh start guest-vm.example.org 

Then in the guest, we have to resize the physical volume. The VM 
should see the data logical volume as /dev/vdb, and the main system as /dev/vda.

First, we have to resize the physical volume::

    pvresize /dev/vdb

Then the volume need to be resized::

    lvresize /dev/mapper/guest-data

And finally, grow the filesystem. This step depend on the filesystem used. For
example, for xfs, the command would be::

    xfs_growth /dev/mapper/guest-data

Step 4: reflect the change in the playbook
------------------------------------------

If any change is done, it should be reflected in the playbook. There
is usually something to change on the hypervisor playbook, and depending
on the VM, in the playbook to deploy the VM or any filesystem deployed there.
