DNS
===

DNS is currently hosted by Red Hat IT, on Red Hat hosted servers. While being
less than ideal from a openess point of view, we currently do not have the required
ressources to replace that, and due to the criticity of DNS, this is not a priority
to be changed.

To modify it, someone with access to the internal dns-maps server need to send the commit.

The current list of persons with access are::

 i. Michael Scherer
 ii. Nigel Babu

If needed, RH IT can also do a modification and/or grant access.

Naming conventions
------------------

In order to be able to use specific domain name matching with ansible, the following naming
convention is used.

For ip hosted in Rackspace cloud, we use ``*.rax.gluster.org``.

For ip in the Community cage, we use ``*.rht.gluster.org``.

If the ip is internal and on the VLAN 401 (Common, also called Internal), the domain
should be ``*.int.rht.gluster.org``.

If the ip is on the VLAN 400 (Management, also called Admin), the domain should be
``*.adm.rht.gluster.org``.

Historical servers may use ``*.rack.gluster.org`` and ``*.cloud.gluster.org``, but newer servers
no longer use this. We try to keep the ``*.gluster.org`` naming for externally visible name.
Ideally, they should only be used for CNAME on real server name. This is done to permit potential
migration or change without impacting external users.

