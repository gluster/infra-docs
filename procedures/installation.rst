Installation of a new server
============================

All new servers must be put into the pool of ansible managed 
server. For that, once the server is installed and a admin has ssh
access, the following procedure is used to let ansible manage it.

Step 1: Openssh
===============

Disable root login with a password as soon as possible. Ansible will take
care of that, but better be sure.

For that, make sure that the sshd configuration contain::

    PermitRootLogin without-password

Step 2: Upgrade
===============

Upon installation, make sure that the server is upgraded to the
latest security patches. Exact syntax depend on the OS, report to the
documentation of the system. Do not forget to reboot after.

Step 3: Install salt and connect to salt-master
===============================================

For a Centos 7 host named server.example.org, as root::

    yum install -y epel-release
    yum install -y salt-minion
    service salt-minion start 
    echo master: salt-master.gluster.org >> /etc/salt/minion
    service salt-minion restart

Then on the salt-master host, as root::

    salt-key -a server.example.org

Test connectivity with::

    su - ansible_admin
    ansible all -i 'server.example.org,' -e 'ansible_connection=saltstack' -m ping

it should answer something like this::

    server.example.org | SUCCESS => {
        "changed": false, 
        "ping": "pong"
    }

Then basic configuration can be deployed with::

    su - ansible_admin
    ansible-playbook -i 'server.example.org,' -e 'ansible_connection=saltstack' /etc/ansible/playbooks/deploy_base.yml 

Step 4: Add it to ansible
=========================

To add the server to ansible, you need to have a checkout of the ansible repo, report to the
ansible documentation for instruction.

Then you just need to add to the hosts file, in the appropriate group, and push (and/or make a PR).



