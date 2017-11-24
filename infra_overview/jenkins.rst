Jenkins
=======

We use Jenkins to run smoke tests, regression tests, build the release tarball,
and to build RPMs.  It is hosted on myrmicinae.rht.gluster.org in RDU. We track
the continous updates on the LTS channel provided by Jenkins.

* URL: https://build.gluster.org
* Current Version: 2.73.3
* Date of Upgrade: 2017-11-09

Plugins
-------

The plugins of note are the following:

* Gerrit trigger
* Job configuration history plugin
* Audit trail
* Git plugin

Access
------

Access to Jenkins is via Github. The admins are added directly on the Jenkins
UI based on a Github username. To add an admin, they need to first use Github
to login to Jenkins so their user is created.

Gluster release managers and some developers have write access to selected
parts of the Jenkins user interface through the jenkins-admins team on Github.
Unless someone is a part of the Gluster CI team, this is the higest level of
access they will be granted.

Managing Jenkins jobs
---------------------

Jenkins jobs are managed with `Jenkins Job Builder`_. Editing existing jobs or
adding new jobs are managed by submitting patches to the `build-jobs`_
repository. A Jenkins job called ``jenkins-update`` will run ``jenkins-jobs
update`` when a patch is merged via Gerrit to the repo. This will not run on
a direct push to master, however.

.. _Jenkins Job Builder: https://docs.openstack.org/infra/jenkins-job-builder/
.. _build-jobs: https://review.gluster.org/#/admin/projects/build-jobs
