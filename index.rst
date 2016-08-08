Gluster infrastructure
======================

This website is meant to serve as the source of truth about gluster project's
infrastructure. It describes our tools and general operational procedures.


.. toctree::
   tools/index
   procedures/index
   :maxdepth: 2

Infrastructure Responsibility Matrix
------------------------------------
The section aims to define ownership and point of contact for issues.

OSAS Sysadmin
'''''''''''''
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
     - OSAS Sysadmin
   * - supercolony.gluster.org
     - OSAS Sysadmin
   * - webbuilder.gluster.org
     - OSAS Sysadmin
   * - munin.gluster.org
     - OSAS Sysadmin
   * - download01.gluster.org
     - OSAS Sysadmin
   * - freeipa01.gluster.org
     - OSAS Sysadmin
   * - syslog01.gluster.org
     - OSAS Sysadmin
   * - Infra Security Issues
     - OSAS Sysadmin and Gluster CI Engineer

**Note**: Nigel is only responsible for the Gerrit software and Jenkins
software. The uptime, OS updates, and OS upgrades are all owned by the OSAS
team.

Who to Contact for What
-----------------------

.. list-table:: Point of Contact
   :widths: 50 50
   :header-rows: 1

   * - Situation
     - Contact
   * - Gerrit/Jenkins Outage
     - OSAS Sysadmin Team
   * - Gerrit/Jenkins Issues (not an outage)
     - Gluster CI Engineer
   * - Access to machines
     - OSAS Sysadmin Team
   * - Access to build nodes (previously called slaves)
     - Gluster CI Engineer
   * - Infra-related build failures
     - Gluster CI Engineer
   * - Infra Security Issues
     - OSAS Sysadmin and Gluster CI Engineer

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
