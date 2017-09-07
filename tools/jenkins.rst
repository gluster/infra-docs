Jenkins
=======

We use Jenkins to run smoke tests, regression tests, build the release tarball,
and to build RPMs.  It is hosted on formicary.gluster.org in the RDU.

* URL: https://build.gluster.org
* Current Version: 1.653
* Date of Upgrade: <unknown>

Plugins
-------

The plugins of note are the following:

* Gerrit trigger
* Job configuration history plugin
* Audit trail
* Git plugin

Access
------

There are two unix groups used to grant access to people:

* **jenkinsadmins**: This group has full access to Jenkins to manage Jenkins itself
  and edit jobs.
* **jenkinsusers**: This group has access to retrigger jobs and read job
  configuration.

To add a user to one of these groups, add them like this::

    usermod -a -G jenkinsadmins nigelb
