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
The section aims to define ownership and point of contact for issues in
the infrastructure team. Currently, there is 2 separates roles in order
to let people focus on specific area.

Sysadmin
''''''''
Michael Scherer

CI Engineer
'''''''''''
Nigel Babu

.. list-table:: Infrastructure Responsibility
   :widths: 50 50
   :header-rows: 1

   * - Product
     - Owner
   * - Gerrit (review.gluster.org)
     - CI Engineer
   * - Jenkins (build.gluster.org)
     - CI Engineer
   * - Build Nodes
     - CI Engineer
   * - Mailling lists
     - Sysadmin
   * - download01.gluster.org
     - Sysadmin   
   * - Generic infrastructure
     - Sysadmin
   * - Infra Security Issues
     - Sysadmin and CI Engineer

**Note**: CI Engineer is only responsible for the Gerrit software and Jenkins
software. The uptime, OS updates, and OS upgrades are all owned by the Sysadmin.

Who to Contact for What
-----------------------

.. list-table:: Point of Contact
   :widths: 50 50
   :header-rows: 1

   * - Situation
     - Primary Contact
   * - Gerrit/Jenkins Outage
     - Sysadmin
   * - Gerrit/Jenkins Issues (not an outage)
     - CI Engineer
   * - Access to machines
     - Sysadmin
   * - Access to build nodes (previously called slaves)
     - CI Engineer
   * - Infra-related build failures
     - CI Engineer
   * - Infra Security Issues
     - Sysadmin and CI Engineer

If the primary contact is not present (days off, holidays, sick), another member of the infrastructure team can 
take a look and solve issues. Everybody in the infra team has the same access, and if anything is missing for a member,
this is a bug and should be fixed.


Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
