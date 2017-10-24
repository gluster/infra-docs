Removing a VM
=============

VM removal is not a automated process, due to risk involved, usage of systems
outside of ansible reach and unfrequent needs.


Step 0: Do backups and verify the VM is not needed
--------------------------------------------------

In order to avoid errors, we should always verify that the VM is really not needed, and
make sure we have backups of whatever is needed on that VM. Backups should be done automatically,
but the coverage is not perfect yet, so better double check.

Step 1: Shutting down the VM
----------------------------

In order to verify nothing break, the VM should be shutdown first and we should
wait to verify nothing broke. Dependin on the VM, we can wait a few hours to a few days.

Step 2: Remove the VM from ansible
----------------------------------

The VM need to be removed from ansible hosts file.
Edit the 'hosts' file and remove the VM from all groups where it appear.

Step 3: Remove it from all playbooks
------------------------------------

After a VM removal, if a group is empty, it should be removed, and corresponding
playbooks must also be erased. Since all is in git, this can always be reinstated.
 
Step 4: Clean the DNS
---------------------

For now, the DNS is managed by RH IT. Please contact a admin to get them modify the
internal dns-maps repository. Both the gluster.org zone and reverse zone must be modified.

Step 5: Clean up the ssh key from ansible bastion
-------------------------------------------------

To avoid issue in the future is the system is reinstalled, the ssh key need to be removed
from the ssh know_hosts file on the ansible bastion.

To do that, connect on the bastion as a regular user::

     ssh ant-queen.int.rht.gluster.org

Then use clean_ssh_public_keys.py to clean it::

     sudo -u ansible_admin /usr/local/bin/clean_ssh_public_keys.py oldvm.example.com

Step 6: Clean up of the other systems
-------------------------------------

Depending on the system, several others things need to be cleaned.

For example, the definition of the host need to be removed from FreeIPA.
The backup need to be removed if needed, the same go for the logs. 

We currently do not have documentation for that, so please contact admins.

Step 7: Removal of the VM
-------------------------

Finally, once we are sure that we no longer ever need the VM or any data on it,  you can use virsh
on the hypervisor::

     virsh undefine  --remove-all-storage oldvm.example.com

Beware, this will also remove the 2nd drive and any attached drive on the VM. Please be cautious.
