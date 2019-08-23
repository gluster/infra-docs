Gluster infrastructure
======================

This website is meant to serve as the source of truth about gluster project's
infrastructure. It describes our tools and general operational procedures.


.. toctree::
    infra_overview/index
    procedures/index
    emergency
    contributing
    :maxdepth: 2

Infrastructure Responsibility Matrix
------------------------------------
The section aims to define ownership and point of contact for issues.

Gluster Sysadmin
''''''''''''''''
Michael Scherer

Gluster CI Engineer
'''''''''''''''''''
Deepshikha Khandelwal

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
   * - supercolony.rht.gluster.org
     - Sysadmin
   * - all gluster.org not in others categories
     - Sysadmin
   * - download.rht.gluster.org
     - Sysadmin
   * - Infra Security Issues
     - Sysadmin and Gluster CI Engineer

**Note**: Deepshikha is only responsible for the Gerrit software and Jenkins
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
