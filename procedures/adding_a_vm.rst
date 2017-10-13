Adding a new VM using ansible
=============================

VM creation is fully automated using a custom role that will create the VM, using
virt-install.

Step 1: Adding the VM to the DNS
--------------------------------

For the time being, DNS is managed by RH IT, but they did delegate the modification
to members of the community.

So the first step is to decide the ip address to use, and change it in the reverse DNS
and the forward zone in the internal dns-maps repository.

Please refer to the networking documentation to choose a ip, or contact a admin.

Step 2: Creating the VM
-----------------------

In order to create the VM, we need to have:
- an IP address and network setup
- the distribution to be used (with a version)
- the number of CPU (optional, 1 by default)
- the size of the main disk
- the size of a data disk (optional)
- the size of the ram
- the hostname
- the hypervisor where it should be installed

For the hypervisor, we are installing Jenkins builder VMs on haplometrosis and pleometrosis, and infrastructure
VMs on myrmicinae and formicary. If installing redundant services, please make sure to install on 2 differents
hypervisors.

For network parameters, please refer to the networking documentation to get the right gateway and ip.

By convention, we try to place all VM installation role in a separate role whose name end with '_vm.yml'.

The bridge parameter indicated the primary network to which the VM would be connected. Due to historical reasons,
the bridge name are not consistent on the whole set of servers, so this has been abstracted in variables defined
in hostvars ( such as host_vars/myrmicinae.rht.gluster.org/network_interfaces.yml ). 

To connect to the external public facing network (VLAN 190), you need to use the bridge defined by `bridge_public`.

To connect to the internal private network (VLAN 401), you need to use the bridge defined by `bridge_common`.

Then, a deploy playbook must be added to the ansible repository in 'playbooks/' directory, using the
guest_virt_install role. For a example, please see playbooks/deploy_gerrit_vm.yml and the documentation of the
role for more explanation on the arguments on https://gitlab.com/osas/ansible-role-guest_virt_install

Once the role is written, it can be pushed to the bastion, which would trigger the deployment
automatically. It may take 10 to 20 minutes to finish the run.

Step 3: Adding the VM to the inventory
--------------------------------------

Once the VM is properly installed, it can be added to the inventory file (file hosts in the ansible public repository).

The VM host must also be added to either 'community_cage' group, for public facing servers, or to 'int_rht_gluster_org' 
group if plugged on the internal network.

Upon sending the commit to the bastion server, ansible will take care of triggering any role that requires to be deployed
there, and add the ssh key to known_hosts if needed.
