Salt
====

Salt was the first configuration management system used by
the project. A migration to ansible is on going at the moment
(June 2016), but salt is still used as a transport mechanism for now

The main server is salt-master.gluster.org and run a salt-master, on 
a Centos 7 with EPEL packages.

it is currently hosted in the Rackspace cloud.

Repository with salt formula 
----------------------------

The repository with the salt formulas can be found on github:

https://github.com/gluster/gluster.org_salt_states/

Pillar informations are on: 

https://github.com/gluster/gluster.org_salt_pillar

No development is expected to occurs on that repositories, and formulas
are being converted to ansible slowly.

Integration with ansible
------------------------

Salt can still be used for most servers, but is not supposed
to be used anymore. Ansible use a connexion plugin to send order
on the salt bus, which is a rather non standard setup but working well
most of the time. The plugin can be found on:
 
https://github.com/OSAS/ansible-role-salt_transport

Links
-----

Thread about switching from Salt to ansible
https://www.gluster.org/pipermail/gluster-infra/2016-January/001594.html
