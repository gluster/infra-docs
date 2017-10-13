Finding network information in the Community cage
=================================================

To find which port is connected to each VLAN, tshark and lldp
announces can be used.

Step 1: Connect to the hypervisor as root
-----------------------------------------

All hypervisor are connected to the public internet for now. So ssh
as root is sufficient::

    $ ssh root@server.example.com

Step 2: Run tcpdump to capture traffic
--------------------------------------

The switches announce information using the Link Layer Discovery Protocol,
that can be printed using specific tool or tshark, the command line version
of wireshark.

However, on EL7, tshark come with wireshark, which pull a complete GTK and X11 stack,
and we want to avoid it. It is also safer to not run tshark as root due to the complexity of
the parser and past security issues.

So the recommended approach is to dump network using tcpdump, then locally look with tshark.

To find for example which vlan is on virbr2, the command line would be::

    # tcpdump -i virbr2 -w /tmp/dump not ip and not arp and not stp

After enough time (something like 30s to 1 minute), stop tcpdump with Ctrl-C

Step 3: Dissect the dump with tshark
------------------------------------

Copy the file using scp::

    $ scp root@server.example.com:/tmp/dump /tmp/dump

Verify with tshark the content::

    $ tshark -r /tmp/dump -Y lldp
    24          11 JuniperN_fe:f4:30 -> LLDP_Multicast LLDP 378 Chassis Id = 5c:43:27:ef:f8:04 Port Id = ge-1/0/43 TTL = 120 System Name = sw02-access-r3-06-b01

Here, we can see that the that the switch were that interface is connected is 'sw02-access-r3-06-b01', the port is 'ge-1/0/43'

Once the information is found, do not forget to remove the dump::

   $ rm -f /tmp/dump
   $ ssh root@server.example.com rm -f /tmp/dump

