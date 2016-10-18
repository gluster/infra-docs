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

Step 2: Creating the VM
-----------------------

In order to create the VM, we need to have:
- an IP address
- the distribution to be used (with a version)
- the number of CPU
- the size of the main disk
- the size of the ram
- the name
- the server where it should be installed

For now, we are installing Jenkins VM on haplometrosis and pleometrosis, and infrastructure
VM on myrmicinae and formicary.

Then, a deploy playbook must be added to the ansible repository in playbooks, using the guest_virt_install
role. For a example, please see playbooks/deploy_gerrit_vm.yml and the documentation of the role on
for more explanation on the arguments on https://gitlab.com/osas/ansible-role-guest_virt_install

The bridge parameters would most of the time be virbr1, but in doubt, ask to the 
sysadmins to verify.

Once the role is written, it can be pushed to the bastion, which would trigger the deployment
automatically. It may take 10 to 20 minutes to finish it.

Step 3: Adding the VM to the inventory
--------------------------------------

Once the VM is properly installed, it can be added to the inventory file (file hosts in the ansible public repository). 

The VM host must be added to at least 'community_cage' group, and likely to 'managed_by_ssh'.

Upon sending the commit to the bastion server, ansible will take care of triggering any role that requires to be deployed
there, and add the ssh key to known_hosts if needed.

Step 4: Deploy the base configuration (optional)
------------------------------------------------

For now, we have to do the first deployment manually if the VM do not have a specific role assigned,
due to the way our repository is layed out, or wait until the regular night job during the night.

A sysadmin have to connect to the bastion (salt-master.gluster.org), and then
the basic configuration can be deployed with::

    su - ansible_admin
    ansible-playbook /etc/ansible/playbooks/deploy_base.yml -l server.example.org
