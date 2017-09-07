Salt
====

Salt was the first configuration management system used by the project.
A migration to ansible was done and completed as of September 2016 
and used as a transport mechanism for now

The main server is salt-master.gluster.org and runs salt-master on Centos
7 with EPEL packages.

It is currently hosted in Rackspace cloud.

Archives repository with salt formula
---------------------------------------

The repository with the salt formulas can be found on github:

https://github.com/gluster/gluster.org_salt_states/

Pillar information is on:

https://github.com/gluster/gluster.org_salt_pillar

The whole repository is currently kept for historical reason,
and shouldn't be used for anything.

Integration with ansible
------------------------

Salt can still be used for most servers, but is not supposed to be used
anymore. Ansible use a connection plugin to send order on the salt bus, which is
a rather non standard setup but working well most of the time. The plugin can
be found on:

https://github.com/OSAS/ansible-role-salt_transport

Links
-----

Thread about switching from Salt to ansible
https://www.gluster.org/pipermail/gluster-infra/2016-January/001594.html
