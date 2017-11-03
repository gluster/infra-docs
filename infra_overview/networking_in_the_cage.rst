Managing networking in the community infrastructure cage
========================================================

Current setup is composed of 4 servers, each with 4 ethernet interfaces.

For various historical reasons, all of them are directly connected to the
internet using the public ip range assigned in the Community Infrastructure
Cage, but we plan to change that.


VLAN description
----------------

Switches and routers are currently managed by RH IT, and so any VLAN change requires
to be asked to their ticket system by someone working at RH. Please contact gluster-infra
list for any change, the admins will take care of that.

The network setup is composed of a few VLANs, each to be used for a separate usage.

The first vlan is the public vlan (ID 190). This is used for public internet access,
on 8.43.85.129 to 8.43.85.190. It is shared with other tenants in the cage.

The 2nd vlan is the "management" vlan (ID 400), sometime also called "admin vlan".
Each hypervisor is connected there, as well as the IPMI or remote admin cards
of the physical servers. Unless exception, no VM should ever be connected here
for security reasons.

The 3rd vlan is the "common" vlan (ID 401), also called "internal vlan".
It is used to connect internal server with non routable IP. Server here have internet
access behind a NAT, but we are moving on tightening the access with a dedicated
firewall managed by us.

IP range assignation
--------------------

+------+------------+----------------+--------------+
| VLAN | Name       | IP Range       | Gateway      |
+------+------------+----------------+--------------+
| 190  | Public     | 8.43.85.128/26 |  8.43.85.254 |
+------+------------+----------------+--------------+
| 400  | Management | 172.24.0.0/24  | 172.24.0.254 |
+------+------------+----------------+--------------+
| 401  | Common     | 172.24.1.0/24  | 172.24.1.181 |
+------+------------+----------------+--------------+


DNS Servers
-----------

Any DNS server can work. Historically, we have used either the one given
by the hosted (Rackspace), or Google Public DNS (8.8.8.8, 8.8.4.4).

There is plan to isolate internal network by forcing to use a specific DNS
resolver, since this can be useful for filtering and forensic later, but nothing
is setup yet.

Firewall setup
--------------

A set of 2 redundant firewalls, `masa.rht.gluster.org` and `mune.rht.gluster.org` have
been setup. The setup is in high availiability, with one of the 2 server being the
active one using a shared floating ip on both side of the firewall.

The firewalls are connected on public and common vlan, and serve for now only to do
NAT for the servers on the common vlan. Due to HA, the servers can be rebooted one at a time
during the day, the other one picking the IP and the routing automatically.

To share connexion state, the 2 firewalls are connected on a 3rd interface on a isolated vlan
numbered 3998.

The shared IP can be obtained by resolving the name `masamune.$domain` for the internal
and external domain ( int.rht.gluster.org and rht.gluster.org ).

There is no filtering for now, but lockdown is planned later.
