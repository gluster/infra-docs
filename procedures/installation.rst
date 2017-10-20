Installation of a new server
============================

All new servers must be put into the pool of ansible managed server. For that,
once the server is installed and a admin has ssh access, the following
procedure is used to let ansible manage it.

Step 1: Openssh
---------------

Disable root login with a password as soon as possible. Ansible will take care
of that, but better be sure.

For that, make sure that the sshd configuration contain::

    PermitRootLogin without-password

Step 2: Upgrade
---------------

Upon installation, make sure that the server is upgraded to the latest security
patches. Exact syntax depend on the OS, report to the documentation of the
system. Do not forget to reboot after.

Step 3: Install the ssh keys
----------------------------

On ansible bastion, locate the public key used by Ansible for
deployment. It should be in ~ansible_admin/.ssh/id_rsa.pub

Place it on the new server in /root/.ssh/authorized_keys::

    ssh server.example.org mkdir -p /root/.ssh
    ssh server.example.org chmod 700 /root/.ssh
    ssh ant-queen.int.rht.gluster.org cat ~ansible_admin/.ssh/id_rsa.pub | ssh server.example.org tee /root/.ssh/authorized_keys

Test connectivity on the bastion with::

    su - ansible_admin
    ansible all -i 'server.example.org,' -m ping

it should answer something like this::

    server.example.org | SUCCESS => {
        "changed": false,
        "ping": "pong"
    }

Then basic configuration can be deployed with::

    su - ansible_admin
    ansible-playbook -i 'server.example.org,' /etc/ansible/playbooks/deploy_base.yml

Step 4: Add it to ansible inventory
-----------------------------------

To add the server to ansible, you need to have a checkout of the ansible repo,
report to the ansible documentation for instruction.

Then you just need to add to the hosts file, in the appropriate group, and push
(and/or make a PR).
