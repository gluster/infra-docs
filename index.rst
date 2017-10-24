Gluster infrastructure
======================

This website is meant to serve as the source of truth about gluster project's
infrastructure. It describes our tools and general operational procedures.


.. toctree::
    infra_overview/index
    procedures/index
    emergency
    :maxdepth: 2

Infrastructure Responsibility Matrix
------------------------------------
The section aims to define ownership and point of contact for issues.

Gluster Sysadmin
''''''''''''''''
Michael Scherer

Gluster CI Engineer
'''''''''''''''''''
Nigel Babu

.. list-table:: Infrastructure Responsibility
   :widths: 50 50
   :header-rows: 1

   * - Product
     - Owner
   * - Gerrit
     - Gluster CI Engineer
   * - Jenkins
     - Gluster CI Engineer
   * - Build Nodes
     - Gluster CI Engineer
   * - salt-master.gluster.org
     - Sysadmin
   * - supercolony.gluster.org
     - Sysadmin
   * - webbuilder.gluster.org
     - Sysadmin
   * - munin.gluster.org
     - Sysadmin
   * - download01.gluster.org
     - Sysadmin
   * - freeipa01.gluster.org
     - Sysadmin
   * - syslog01.gluster.org
     - Sysadmin
   * - Infra Security Issues
     - Sysadmin and Gluster CI Engineer

**Note**: Nigel is only responsible for the Gerrit software and Jenkins
software. The uptime, OS updates, and OS upgrades are all owned by the Sysadmin team.

Who to Contact for What
-----------------------

.. list-table:: Point of Contact
   :widths: 50 50
   :header-rows: 1

   * - Situation
     - Contact
   * - Gerrit/Jenkins Outage
     - Sysadmin Team
   * - Gerrit/Jenkins Issues (not an outage)
     - Gluster CI Engineer
   * - Access to machines
     - Sysadmin Team
   * - Access to build nodes (previously called slaves)
     - Gluster CI Engineer
   * - Infra-related build failures
     - Gluster CI Engineer
   * - Infra Security Issues
     - Sysadmin and Gluster CI Engineer

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
