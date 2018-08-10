Gerrit
======

We use Gerrit as the primary place for hosting code and conducting code
reviews. It is hosted on myrmicinae.rht.gluster.org in RDU.

* URL: https://review.gluster.org
* Current Version: 2.15.3
* Date of Upgrade: 2018-08-10

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


Authentication Issues
---------------------

In June 2016, we upgraded Gerrit from 2.9 to 2.12.2. This caused login
issues for a lot of users. In older versions of Gerrit, users could set
a username after login. In newer versions, not only did this ability go away,
Gerrit required that your Gerrit username must match your Github username. It
would throw an error if your Gerrit username and Github username were not the
same. To fix this, `we changed`_ everyone's Gerrit username to match their
Github username. This cleared up the issues for everyone who had trouble back
then.

In the recent months, we've noticed that when some of the previously active
users tried to sign in, they'd run into troubles that looked very much like the
old problems. The easiest solution has been to find their old account and
remove the entries from ``accounts_external_ids`` table. Changing the username
entries on Gerrit does not seem to work anymore. I recommend attempting this on
staging first and confirming all is well before trying on production.

Gerrit has completely switched to NoteDB for User information, so any hacks we
had that needed PostgreSQL queries will not work anymore.
.. _login issues: https://lists.gluster.org/pipermail/gluster-infra/2016-June/002227.html
.. _we changed: https://lists.gluster.org/pipermail/gluster-infra/2016-June/002239.html
