Gerrit
======

We use Gerrit as the primary place for hosting code and conducting code
reviews. It is hosted on formicary.gluster.org in the RDU.

* URL: https://review.gluster.org
* Current Version: 2.12.2
* Date of Upgrade: 01-06-2016

Plugins
-------

When upgrading, remember the plugin version should match the version of Gerrit.
We have the following plugins installed on our instance (apart from the default
ones):

* `Github <https://gerrit.googlesource.com/plugins/github/+/master/README.md>`_
  (only the oauth library, not the plugin)
* `Events log <https://gerrit.googlesource.com/plugins/events-log/>`_
* `Replication <https://gerrit.googlesource.com/plugins/replication/+/master/src/main/resources/Documentation/about.md>`_

Replication
-----------

Two repositories from our instance are replicated onto Github

* glusterfs
* glusterfs-specs
